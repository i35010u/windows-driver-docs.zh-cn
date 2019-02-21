---
title: 查找失败的进程
description: 查找失败的进程
ms.assetid: 64d1fa71-940f-4f67-87a6-00d41d6f24e0
keywords:
- 过程中，查找失败的进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b13581d75dcb0a68d9b8840af69f741a90b38ec8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525326"
---
# <a name="finding-the-failed-process"></a>查找失败的进程


## <span id="ddk_finding_the_failed_process_dbg"></span><span id="DDK_FINDING_THE_FAILED_PROCESS_DBG"></span>


查找进程失败之前, 请确保您已接受的处理器的上下文中。 若要确定正在接受处理器，请使用[ **！ pcr** ](-pcr.md)上每个处理器的扩展，然后查找为其加载异常处理程序的处理器。 接受处理器的异常处理程序具有非 0xFFFFFFFF 地址。

例如，因为地址**NtTib.ExceptionList**此处理器是 0xFFFFFFFF，这是不具有失败的进程的处理器：

```dbgcmd
0: kd> !pcr 
PCR Processor 0 @ffdff000
 NtTib.ExceptionList: ffffffff
            NtTib.StackBase: 80470650
           NtTib.StackLimit: 8046d860
         NtTib.SubSystemTib: 00000000
              NtTib.Version: 00000000
          NtTib.UserPointer: 00000000
              NtTib.SelfTib: 00000000

                    SelfPcr: ffdff000
                       Prcb: ffdff120
                       Irql: 00000000
                        IRR: 00000000
                        IDR: ffffffff
              InterruptMode: 00000000
                        IDT: 80036400
                        GDT: 80036000
                        TSS: 80257000

              CurrentThread: 8046c610
                 NextThread: 00000000
                 IdleThread: 8046c610

                  DpcQueue: 
```

但是，处理器 1 的结果是完全不同。 在本示例中的值**NtTib.ExceptionList**是**f0823cc0**，不 0xFFFFFFFF，指示这发生了异常的处理器。

```dbgcmd
0: kd> ~1 
1: kd> !pcr
PCR Processor 1 @81497000
 NtTib.ExceptionList: f0823cc0
            NtTib.StackBase: f0823df0
           NtTib.StackLimit: f0821000
         NtTib.SubSystemTib: 00000000
              NtTib.Version: 00000000
          NtTib.UserPointer: 00000000
              NtTib.SelfTib: 00000000

                    SelfPcr: 81497000
                       Prcb: 81497120
                       Irql: 00000000
 IRR: 00000000
                        IDR: ffffffff
              InterruptMode: 00000000
                        IDT: 8149b0e8
 GDT: 8149b908
                        TSS: 81498000

              CurrentThread: 81496d28
                 NextThread: 00000000
                 IdleThread: 81496d28

                  DpcQueue: 
```

在正确的处理器上下文中，当[ **！ 过程**](-process.md)扩展显示当前正在运行的进程。

进程转储的最有趣的部分是：

-   （较高的值指示进程可能是罪魁祸首） 时间。

-   句柄计数 (这是后的括号中的数字**对象表**中的第一个条目)。

-   线程状态 （多个进程具有多个线程）。 如果当前进程*空闲*，它是可能的计算机是真正空闲或它挂起由于一些异常问题。

尽管使用 **！ 处理 0 7**扩展是挂起的系统上找出问题的最佳方法，而有时是太多的信息进行筛选。 请改用 **！ process 0 0** ，然后 **！ 过程**上 CSRSS 和任何其他可疑进程的进程句柄。

使用时 **！ 处理 0 7**，很多线程可能被标记为"未驻留的内核堆栈"因为这些堆栈调出。如果这些页仍处于过渡状态在缓存中，您可以通过使用获取详细信息 **.cache decodeptes**之前 **！ 处理 0 7**:

```dbgcmd
kd> .cache decodeptes 
kd> !process 0 7 
```

如果可以标识故障进程，请使用 **！ 过程** *&lt;进程&gt;* **7**过程中显示每个线程的内核堆栈。 此输出可以确定在内核模式下问题并显示可疑进程正在调用。

除了 **！ 过程**，以下扩展可帮助以确定响应的计算机的原因：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">扩展</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><a href="-ready.md" data-raw-source="[!ready](-ready.md)">!ready</a></strong></p></td>
<td align="left"><p>标识已准备好运行，按优先顺序的线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-locks---kdext--locks-.md" data-raw-source="[!kdext*.locks](-locks---kdext--locks-.md)">!kdext*.locks</a></strong></p></td>
<td align="left"><p>标识任何持有的资源锁，以防出现死锁与零售的超时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-vm.md" data-raw-source="[!vm](-vm.md)">!vm</a></strong></p></td>
<td align="left"><p>检查虚拟内存使用情况。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-poolused.md" data-raw-source="[!poolused](-poolused.md)">!poolused</a></strong></p></td>
<td align="left"><p>确定是否有一种池分配为极大 （池标记所需）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-memusage.md" data-raw-source="[!memusage](-memusage.md)">!memusage</a></strong></p></td>
<td align="left"><p>检查物理内存状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-heap.md" data-raw-source="[!heap](-heap.md)">!heap</a></strong></p></td>
<td align="left"><p>检查堆的有效性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-irpfind.md" data-raw-source="[!irpfind](-irpfind.md)">!irpfind</a></strong></p></td>
<td align="left"><p>搜索 active Irp 非分页缓冲的池。</p></td>
</tr>
</tbody>
</table>

 

如果提供的信息并不表示异常条件，请尝试设置一个断点处**ntoskrnl ！KiSwapThread**来确定处理器是否停滞在一个进程，或如果它仍计划其他进程。 如果没有卡，在中设置断点公共函数，如**NtReadFile**，以确定计算机是否停滞在特定的代码路径。

 

 





