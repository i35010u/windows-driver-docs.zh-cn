---
title: 使用日志记录跟踪重要的事件
description: 使用日志记录跟踪重要的事件
ms.assetid: 297336c2-85fb-4235-a7ab-0bbf571b8b98
keywords:
- 流式处理调试的内核，视频流停滞，日志记录
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc8b7ee79e43c7e50043218a41f278cc51753eb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554876"
---
# <a name="using-logging-to-track-important-events"></a>使用日志记录跟踪重要的事件


一般情况下，仅通过触发事件、 微型驱动程序的处理和缓冲区完成下游移动数据。 若要找出了挂起的原因或停滞的程序：

- 检查是否有不匹配**KsGate * Xxx*** 调用。

- 检查省略**Ks*Xxx*AttemptProcessing**调用。

- 外观的与触发事件，包括相关的代码中的问题或者代码的引用为问题的流的 pin 标志或调用**KsPinAttemptProcessing**。

- 查找与相关的代码处理调度，特别是在排队进入硬件以及创建克隆指针中的问题。

- 查找与驱动程序的相关的代码中的问题延迟过程调用 (DPC)，尤其是在缓冲区都已完成或任何在调用[KsStreamPointerDelete](https://go.microsoft.com/fwlink/p/?linkid=56550)。

- 查找流的启动代码中的问题。

收集此信息的最有效方法是通过记录的所有内容在受影响区域中，包括处理 （如克隆和编程硬件） 的缓冲区获取缓冲区 （如删除克隆），版本和入口的任何操作。 大多数此类信息是高度时间有关，需要基于内存的日志记录或 ETW。

若要维护滚动的基于内存的日志，使用以下代码：

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
```dbgcmd

Then, use a simple "dc g\_Log" to view the contents of the **g\_Log** array in the debugger.

The following example uses the above memory-based scheme to determine the cause of a processing stall. Output is from an AVStream streaming scenario in graphedt. The following minidriver events were logged:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Abbreviation</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>Strt</em></p></td>
<td align="left"><p>This event occurs when the minidriver first queues buffers for the device from within the minidriver's <em>Start</em> dispatch.</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Prc&lt;</em></p></td>
<td align="left"><p>This event occurs at the start of the minidriver's <em>Process</em> dispatch.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>AddB</em></p></td>
<td align="left"><p>This event occurs when the minidriver queues buffers to the device from within its <em>Process</em> dispatch.</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DPC&lt;</em></p></td>
<td align="left"><p>This event occurs at the start of the minidriver's <em>CallOnDPC</em>. It indicates buffer completion.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Atmp</em></p></td>
<td align="left"><p>This event occurs when the minidriver calls from within the DPC to <strong>KsPinAttemptProcessing</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Dele</em></p></td>
<td align="left"><p>This event occurs when the minidriver calls from within the DPC to delete a clone stream pointer.</p></td>
</tr>
</tbody>
</table>

 

Log excerpts are as follows:

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

此第一个日志摘录是在代表正常的流式处理状态。 在第一行，微型驱动程序的*CallOnDPC*调用以完成一个缓冲区 (*DPC&lt;*)。 删除缓冲区 (*Dele*)，并**KsPinAttemptProcessing**称为向前前沿，如果队列中有任何未处理的缓冲区 (*Atmp*)。 在这种情况下，有个，可以看出过程调度调用 (*中国&lt;*)。 向队列中添加更多的缓冲区 (*AddB*)，并重复整个方案。

此下一步摘录右日志中包括的最后一个条目之前停止出现。

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

在此示例中，完成多个缓冲区 (所指示的重复实例*DPC&lt;*)，但有任何未处理的缓冲区在队列中，因此未被调用过程调度 (由缺少*中国&lt;*)。 事实上，所有的队列中已处理的缓冲区都完成后，显然之前无法添加任何新的未处理的缓冲区。 因为已在运行该应用程序 (以便*启动*将不会调用) 和对进行任何调用都不*CallOnDPC* （因为有未处理的缓冲区准备好完成），任何新的缓冲区很明显的前导边缘，等待处理，不含任何内容启动处理之前累积。

问题在于 KSPIN\_标志\_不要\_不\_启动\_设置处理标志。 通过调用仅当设置此标志后, 进行处理*启动*或*CallOnDPC*。 如果未设置此标志，每当新缓冲区添加到队列时，将会启动处理。

 

 





