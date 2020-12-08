---
title: 查找失败的进程
description: 查找失败的进程
keywords:
- 处理，查找失败的进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83f9bc41cf2c18a973e8cc326e9f656a86ea9037
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838189"
---
# <a name="finding-the-failed-process"></a>查找失败的进程


## <span id="ddk_finding_the_failed_process_dbg"></span><span id="DDK_FINDING_THE_FAILED_PROCESS_DBG"></span>


在查找失败的进程之前，请确保你处于接受处理器的上下文中。 若要确定接受的处理器，请在每个处理器上使用 [**！ pcr**](-pcr.md) 扩展，并查找已加载异常处理程序的处理器。 接受处理器的异常处理程序的地址不是0xFFFFFFFF。

例如，由于此处理器上的 **NtTib** 的地址为0xffffffff，这并不是失败进程的处理器：

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

但是，处理器1的结果并不完全相同。 在这种情况下， **NtTib** 的值是 **f0823cc0**，而不是0xffffffff，指示这是发生异常的处理器。

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

在正确的处理器上下文中， [**！进程**](-process.md) 扩展显示当前正在运行的进程。

进程转储的最有趣的部分是：

-   较高值 (的时间指示进程可能是) 的原因。

-   句柄计数 (这是第一项) 中 **ObjectTable** 后的括号中的数字。

-   线程状态 (多个进程) 有多个线程。 如果当前进程处于 *空闲状态*，则很可能是计算机真正处于空闲状态，或由于某些异常问题而挂起。

尽管使用 **！ process 0 7** 扩展是查找挂起系统上的问题的最佳方法，但有时要筛选的信息太多。 相反，请使用 **！ process 0 0** ，然后在 CSRSS 和任何其他可疑进程的进程句柄上使用 **！** 进程。

使用 **！进程 0 7** 时，很多线程可能会被标记为 "不驻留内核堆栈"，因为这些堆栈已分页。如果这些页面仍处于正在转换的缓存中，则可以通过使用 **. cache decodeptes** before **！ process 0 7** 获取详细信息：

```dbgcmd
kd> .cache decodeptes 
kd> !process 0 7 
```

如果可以识别失败的进程，请使用 **！ process** *&lt; process &gt;* **7** 显示进程中每个线程的内核堆栈。 此输出可确定内核模式下的问题，并显示可疑进程正在调用的内容。

除 **！进程** 外，以下扩展可帮助确定计算机无响应的原因：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">扩展名</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><a href="-ready.md" data-raw-source="[!ready](-ready.md)">！就绪</a></strong></p></td>
<td align="left"><p>按优先顺序标识已准备好运行的线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-locks---kdext--locks-.md" data-raw-source="[!kdext*.locks](-locks---kdext--locks-.md)">！ kdext *. 锁</a></strong></p></td>
<td align="left"><p>标识所有保留的资源锁，以防出现零售超时的死锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-vm.md" data-raw-source="[!vm](-vm.md)">！ vm</a></strong></p></td>
<td align="left"><p>检查虚拟内存使用情况。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-poolused.md" data-raw-source="[!poolused](-poolused.md)">!poolused</a></strong></p></td>
<td align="left"><p>确定) 是否需要对一种池分配进行大容量 (池标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-memusage.md" data-raw-source="[!memusage](-memusage.md)">!memusage</a></strong></p></td>
<td align="left"><p>检查物理内存状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-heap.md" data-raw-source="[!heap](-heap.md)">！堆</a></strong></p></td>
<td align="left"><p>检查堆的有效性。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-irpfind.md" data-raw-source="[!irpfind](-irpfind.md)">!irpfind</a></strong></p></td>
<td align="left"><p>搜索活动 Irp 的非分页池。</p></td>
</tr>
</tbody>
</table>

 

如果提供的信息未指明异常情况，请尝试在 ntoskrnl.exe 中设置断点 **！KiSwapThread** 确定处理器在一个进程中停滞还是仍在计划其他进程。 如果未阻塞，请在常见函数（如 **NtReadFile**）中设置断点，以确定计算机是否卡在特定代码路径中。

 

 





