---
title: 使用日志记录跟踪重要事件
description: 使用日志记录跟踪重要事件
ms.assetid: 297336c2-85fb-4235-a7ab-0bbf571b8b98
keywords:
- 内核流调试，视频流停止，日志记录
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f269ba5baec6fe1b66d7377673e0c8a215672502
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534752"
---
# <a name="using-logging-to-track-important-events"></a>使用日志记录跟踪重要事件


通常，仅通过触发事件、微型驱动程序的处理和缓冲区完成来移动数据。 确定挂起或延迟的原因：

- 检查不匹配的**KsGate<em>Xxx</em> **调用。

- 检查是否省略了**Ks*Xxx*AttemptProcessing**调用。

- 查找与触发事件相关的代码中的问题，包括引用问题流的 pin 标志或调用**KsPinAttemptProcessing**的代码。

- 查找与处理调度相关的代码中的问题，特别是在它排队到硬件和创建克隆指针的位置。

- 查找与驱动程序的延迟过程调用（DPC）相关的代码中的问题，尤其是在缓冲区完成或对[KsStreamPointerDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)进行任何调用时。

- 查找流的启动代码中的问题。

收集此信息最有效的方法是记录受影响的区域中的所有内容，包括处理、缓冲区获取（如克隆和编程硬件）、缓冲版本（例如删除克隆）和任何入口操作。 此信息的大部分依赖于高时间依赖关系，并需要基于内存的日志记录或 ETW。

若要维护基于滚动内存的日志，请使用以下代码：

```cpp
typedef struct _LOGENTRY {
    ULONG Tag;
    ULONG Arg[3];
} LOGENTRY, *PLOGENTRY;
#define LOGSIZE 2048
LONG g_LogCount;
LOGENTRY g_Log [LOGSIZE];
#define LOG(tag,arg1,arg2,arg3) do { \
    LONG i = InterlockedIncrement (&g_LogCount) % LOGSIZE; \
    g_Log [i].Tag = tag; \
    g_Log [i].Arg [0] = (ULONG)(arg1); \
    g_Log [i].Arg [1] = (ULONG)(arg2); \
    g_Log [i].Arg [2] = (ULONG)(arg3); \
} while (0)
```

然后，使用简单的 "dc g \_ 日志" 在调试器中查看**g \_ 日志**数组的内容。

下面的示例使用上述基于内存的方案来确定处理延迟的原因。 输出来自 graphedt 中的 AVStream 流式处理方案。 已记录以下微型驱动程序事件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">缩写</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>Strt</em></p></td>
<td align="left"><p>当微型驱动程序第一次将设备的缓冲区从微型驱动程序的<em>启动</em>调度中排队时，将发生此事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>中国&lt;</em></p></td>
<td align="left"><p>此事件在微型驱动程序的<em>进程</em>调度开始时发生。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>AddB</em></p></td>
<td align="left"><p>当微型驱动程序将从其<em>进程</em>调度中的设备缓冲区缓冲到设备时，将发生此事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DPC&lt;</em></p></td>
<td align="left"><p>此事件在微型驱动程序的<em>CallOnDPC</em>开始时发生。 它表示缓冲区完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Atmp</em></p></td>
<td align="left"><p>当微型驱动程序从 DPC 内调用<strong>KsPinAttemptProcessing</strong>时，将发生此事件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Dele</em></p></td>
<td align="left"><p>当微型驱动程序从 DPC 内调用来删除克隆流指针时发生此事件。</p></td>
</tr>
</tbody>
</table>

 

日志摘录如下所示：

```text
f9494b80  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f9494b90  656c6544 816e2c90 81750260 00000000  Dele.,n.`.u.....
f9494ba0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f9494bb0  3c637250 819c1f00 00000000 00000000  Prc<............
f9494bc0  42646441 819c1f00 ffa2eb08 00000000  AddB............
f9494bd0  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f9494be0  656c6544 816e2c90 ffa80348 00000000  Dele.,n.H.......
f9494bf0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f9494c00  3c637250 819c1f00 00000000 00000000  Prc<............
f9494c10  42646441 819c1f00 ffa3d9b8 00000000  AddB............
```

此第一个日志摘录代表正常流式处理状态。 在第一行中，将调用微型驱动程序的*CallOnDPC*来完成缓冲区（*DPC &lt; *）。 如果队列中有任何未处理的缓冲区（*Atmp*），则将删除该缓冲区（*Dele*），并调用**KsPinAttemptProcessing**来向前移动前导边缘。 在这种情况下，可以通过调用进程调度（*Prc &lt; *）来查看。 将更多的缓冲区添加到队列（*AddB*），并重复整个方案。

下一摘录包括日志中的最后一项，出现延迟之前。

```text
f949b430  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b440  656c6544 816e2c90 ffac4de8 00000000  Dele.,n..M......
f949b450  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f949b460  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b470  656c6544 816e2c90 816ffc80 00000000  Dele.,n...o.....
f949b480  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f949b490  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b4a0  656c6544 816e2c90 ffa80348 00000000  Dele.,n.H.......
f949b4b0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f949b4c0  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b4d0  656c6544 816e2c90 8174e1c0 00000000  Dele.,n...t.....
f949b4e0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
```

在此示例中，将完成多个缓冲区（由*DPC &lt; *的重复实例指示），但队列中没有未处理的缓冲区，因此不会调用进程调度（由缺少*Prc &lt; *指示）。 事实上，队列中所有已处理的缓冲区已完成，显然在添加任何新的未处理缓冲区之前已完成。 由于应用程序已在运行（因此将不会调用 "*启动*"），并且不会对*CallOnDPC*进行调用（因为没有准备好要完成的已处理的缓冲区），因此，任何新缓冲区都将在前导边缘之前累积，等待处理，无需任何启动处理。

问题在于，KSPIN \_ 标志 \_ \_ 未 \_ 启动 \_ 处理标志。 设置此标志后，仅通过调用*Start*或*CallOnDPC*进行处理。 如果未设置此标志，则每当向队列中添加新缓冲区时都会启动处理。

 

 





