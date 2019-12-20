---
title: Bug 检查 0x1A MEMORY_MANAGEMENT
description: MEMORY_MANAGEMENT bug 检查的值为0x0000001A。 这表明出现了严重的内存管理错误。
ms.assetid: 7d3ff54e-e61a-43fa-a378-fb8d32565586
keywords:
- Bug 检查 0x1A MEMORY_MANAGEMENT
- MEMORY_MANAGEMENT
ms.date: 06/29/2019
topic_type:
- apiref
api_name:
- MEMORY_MANAGEMENT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37a621a1f25f0581ec8bd5da84381209026d77f1
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209319"
---
# <a name="bug-check-0x1a-memory_management"></a>Bug 检查0x1A：内存\_管理


内存\_管理 bug 检查的值为0x0000001A。 这表明出现了严重的内存管理错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="memory_management-parameters"></a>内存\_管理参数

参数1标识完全冲突。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>分叉克隆块引用计数已损坏。 这仅在已选中的 Windows 版本上发生。 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x31</p></td>
<td align="left"><p>映像重定位修复表或代码流已损坏。 这可能是硬件错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3f</p></td>
<td align="left"><p>Inpage 操作失败，出现 CRC 错误。 参数2包含页面文件偏移量。 参数3包含页 CRC 值。 参数4包含预期的 CRC 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x403</p></td>
<td align="left"><p>页面表和 PFNs 不同步。 这可能是硬件错误，尤其是在参数 3 & 4 只是一位不同的情况下。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x404</p></td>
<td align="left"><p>在删除系统页的过程中，页面框架编号（PFN）与当前页表条目（PTE）指针之间存在不一致。 参数2是所需的 PTE。 参数3是 PTE 内容，参数4是 PFN 的 PTE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x411</p></td>
<td align="left"><p>页表项（PTE）已损坏。 参数2是 PTE 的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x777</p></td>
<td align="left"><p>调用方正在解锁当前未锁定的系统缓存地址。 （此地址永远不会映射或解锁两次。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x778</p></td>
<td align="left"><p>系统使用的是最新的系统缓存视图地址，而不是保留它。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x780</p>
<p>0x781</p></td>
<td align="left"><p>映射参数系统缓存视图的 Pte 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p><strong>MmGetSystemAddressForMdl *</strong>的调用方尝试将完全缓存的物理页映射为未缓存。 此操作会导致硬件转换缓冲区出现冲突，因此它被操作系统拒绝。 由于调用方在请求 MDL 中指定了 "失败时 bug 检查"，系统不能选择，而是在此实例中发出 bug 检查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>调用方正在解锁当前未锁定的可分页部分。 （此部分从未锁定或解锁两次。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1233</p></td>
<td align="left"><p>驱动程序尝试映射未锁定的物理内存页。 这是非法的，因为页面的内容或属性随时可能会更改。 这是执行映射调用的代码中的一个 bug。 参数2是驱动程序尝试映射的物理页的页面帧号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1234</p></td>
<td align="left"><p>调用方尝试锁定不存在的可分页部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1235</p></td>
<td align="left"><p>调用方尝试使用无效的映射来保护 MDL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1236</p></td>
<td align="left"><p>调用方指定的 MDL 包含未锁定（或无效）的物理页。 参数2包含指向 MDL 的指针。 参数3包含指向无效 PFN 的指针。 参数4包含无效的 PFN 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3300</p></td>
<td align="left"><p>在执行写入的过程中，被引用的虚拟地址在写入时被错误地标记为副本。 参数2是 FaultingAddress。  参数3是 PTE 内容。 参数4表示虚拟地址空间类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3451</p></td>
<td align="left"><p>已交换的内核线程堆栈的 Pte 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3453</p></td>
<td align="left"><p>由于未完成的引用，无法删除已退出进程的所有页表页。  这通常表示进程的页表结构中的损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4477</p></td>
<td align="left"><p>驱动程序尝试写入系统进程的用户空间中的未分配地址。 参数2包含尝试写入的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5003</p></td>
<td align="left"><p>工作集可用列表已损坏。 这可能是硬件错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5100</p></td>
<td align="left"><p>分配位图已损坏。 内存管理器即将覆盖已在使用中的虚拟地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5200</p></td>
<td align="left"><p>免费池 SLIST 上的页面已损坏。 这可能是驱动程序中的 "无可用" 错误的结果，也可能是上一页的溢出。 参数2包含可用池块的地址。 参数4包含应位于该地址的值。 参数3包含找到的实际值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6001</p></td>
<td align="left"><p>内存存储区组件的专用内存范围已损坏，导致其不可访问。 参数2是返回的状态。  参数3是存储区专用内存范围内的虚拟地址。 参数4为 MemoryDescriptorList。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8884</p></td>
<td align="left"><p>（仅适用于 Windows 7）。 备用列表上的两页应该具有相同的页优先级值，实际上并没有相同的页面优先级值。 参数4中捕获了不同的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8888</p>
<p>0x8889</p></td>
<td align="left"><p>内部内存管理结构已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x888A</p></td>
<td align="left"><p>内部内存管理结构（可能是 PTE 或 PFN）已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9696</p></td>
<td align="left"><p>遇到 PFN （参数2），损坏的链接不再连接到其顶层进程。  这表示 PFN 结构中的损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15001</p></td>
<td align="left"><p>在取消保护以前所保护的内存的过程中出错。  如果调用方错误地在错误的进程上下文中调用 MmUnsecureVirtualMemory，则可能会发生这种情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41201</p></td>
<td align="left"><p>在查询虚拟地址的过程中，页面框架编号（PFN）与当前页表条目（PTE）指针之间存在不一致。 参数2是对应的 PTE。 参数3是 PTE 内容，参数4是虚拟地址描述符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41283</p></td>
<td align="left"><p>在 PTE 中编码的工作集索引已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41284</p></td>
<td align="left"><p>PTE 或工作集列表已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>调用方正在尝试释放无效的池地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41785</p></td>
<td align="left"><p>工作集列表已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41287</p></td>
<td align="left"><p>保存工作集同步时出现非法的页错误。 参数2包含引用的虚拟地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41790</p></td>
<td align="left"><p>页表页已损坏。 在64位版本的 Windows 上，参数2包含损坏的页表页的 PFN 地址。 在32位版本的 Windows 上，参数2包含指向使用的 Pte 数的指针，参数3包含使用的 Pte 数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41792</p></td>
<td align="left"><p>检测到损坏的 PTE。 参数2包含 PTE 的地址。 参数3/4 包含 PTE 的低/高部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41793</p></td>
<td align="left"><p> 页表页已损坏。 参数2包含指向最后处理的 PTE 的指针。 参数3包含找到的非零 Pte 的数目。 参数4包含页表中的预期非零 Pte 数。</p><p>此内存参数已不推荐使用，在 Windows 10 版本1803后不再可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61940</p></td>
<td align="left"><p>PDE 意外失效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61941</p></td>
<td align="left"><p>分页层次结构已损坏。 参数2是指向导致错误的虚拟地址的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61946</p></td>
<td align="left"><p>正在创建的 MDL 有缺陷。 这几乎始终意味着调用<strong>MmProbeAndLockPages</strong>的驱动程序出错。 通常，驱动程序在要求处理分页读取时尝试创建写入 MDL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61948</p></td>
<td align="left"><p>在递减 i/o 空间区域的引用计数的过程中，找不到其会计节点。  通常，这意味着参数范围从未锁定或已解锁。  参数2是基本 i/o 帧。 参数3是区域中的页数，而参数4是找不到其节点的特定 i/o 帧。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61949</p></td>
<td align="left"><p>IoPageFrameNode 为 null。 参数2为 PageFrameIndex。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6194A</p></td>
<td align="left"><p>在对正在取消映射的 i/o 空间物理页上的引用计数进行递减时出错。 正在取消引用当前未引用的项。  参数2和3描述了正在取消映射的调用方的 i/o 空间范围，而参数4是 i/o 空间物理页，它应被引用，但不是。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03030303</p></td>
<td align="left"><p>启动加载程序中断。 （此值仅适用于 Intel Itanium 计算机。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03030308</p></td>
<td align="left"><p>要删除（或截断）的范围正在由加载程序使用，因此无法安全地将其删除，因此系统必须发出 stop 代码。  参数2为 HighestPhysicalPage。</p></td>
</tr>
</tbody>
</table>


<a name="resolution"></a>分辨率
----------

[**！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。 

运行 Windows 内存诊断工具也可用于排除影响物理内存模块的任何类型的问题。
