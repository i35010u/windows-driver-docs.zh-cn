---
title: Bug 检查 0x1A MEMORY_MANAGEMENT
description: MEMORY_MANAGEMENT bug 检查具有 0x0000001A 值。 这表明发生了严重的内存管理错误。
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
ms.openlocfilehash: 8d779e543662bf815ebfd73b68c17f5058151ab7
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492529"
---
# <a name="bug-check-0x1a-memorymanagement"></a>Bug 检查 0x1A：内存\_管理


内存\_管理 bug 检查的值为 0x0000001A。 这表明发生了严重的内存管理错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="memorymanagement-parameters"></a>内存\_管理参数

参数 1 标识了确切的冲突。

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
<td align="left"><p>分叉克隆块引用计数已损坏。 （这仅出现在已检查的 Windows 版本上。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x31</p></td>
<td align="left"><p>映像重定位链接地址表或代码流已损坏。 这可能是硬件错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3f</p></td>
<td align="left"><p>页内操作失败，出现 CRC 错误。 参数 2 包含页面文件偏移量。 参数 3 包含页 CRC 值。 参数 4 包含预期的 CRC 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x403</p></td>
<td align="left"><p>页表和 PFNs 不同步。 这可能是硬件错误，尤其是当参数 3 和 4 上仅有一个位存在差异。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x404</p></td>
<td align="left"><p>正在删除系统页时页帧数 (PFN) 和当前的页表项 (PTE) 指针之间的不一致。 参数 2 是预期的 PTE。 参数 3 为 PTE 内容且参数 4 为 PFN PTE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x411</p></td>
<td align="left"><p>页表项 (PTE) 已损坏。 参数 2 是 PTE 的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x777</p></td>
<td align="left"><p>调用方解锁当前未被锁定的系统缓存地址。 （此地址或者永远不会映射或正在解锁两次。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x778</p></td>
<td align="left"><p>系统正在使用最后一个系统缓存的视图地址，而不保留它。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x780</p>
<p>0x781</p></td>
<td align="left"><p>映射参数系统缓存视图 Pte 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>调用方<strong>MmGetSystemAddressForMdl *</strong>尝试映射完全缓存物理页的非缓存。 此操作将导致冲突的硬件转换缓冲区条目，并因此由操作系统被拒绝。 由于调用方请求 MDL 中指定"失败的 bug 检查"，系统必须以颁发在此实例中的 bug 检查，别无选择。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>调用方解锁当前未被锁定的可分页部分。 （本部分或者永远不会锁定或正在解锁两次。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1233</p></td>
<td align="left"><p>驱动程序尝试映射未锁定的物理内存页面。 这是非法的因为可以在任何时候更改的内容或属性页。 这是进行调用的映射代码中的 bug。 参数 2 是框架驱动程序试图映射的物理页的页码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1234</p></td>
<td align="left"><p>调用方尝试锁定不存在的可分页部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1235</p></td>
<td align="left"><p>调用方尝试保护 MDL 具有无效的映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1236</p></td>
<td align="left"><p>调用方指定 MDL 包含未锁定 （或无效） 的物理页。 参数 2 包含 MDL 的指针。 参数 3 包含无效的 PFN 的指针。 参数 4 包含 PFN 值无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3300</p></td>
<td align="left"><p>过程中执行写入，被引用的虚拟地址被错误地标记为副本在写入。 参数 2 是 FaultingAddress。  参数 3 是 PTE 内容。 参数 4 表示虚拟地址空间类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3451</p></td>
<td align="left"><p>已被换出了内核线程堆栈的 Pte 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3453</p></td>
<td align="left"><p>由于未完成的引用，无法删除已退出进程的所有页表页。  这通常表示进程的页表结构中的损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4477</p></td>
<td align="left"><p>驱动程序尝试写入到系统进程的用户空间中的未分配地址。 参数 2 包含尝试的写入的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5003</p></td>
<td align="left"><p>工作集释放列表已损坏。 这可能是硬件错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5100</p></td>
<td align="left"><p>分配位图已损坏。 内存管理器是以覆盖已使用的虚拟地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5200</p></td>
<td align="left"><p>可用池 SLIST 的页面已损坏。 这可以是驱动程序或从上一页面溢出中写入后无 bug 的结果。 参数 2 包含可用池块的地址。 参数 4 包含应为在该地址的值。 参数 3 包含找到的实际值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6001</p></td>
<td align="left"><p>内存存储组件的专用内存范围已损坏，使其变得不可访问。 参数 2 是返回的状态。  参数 3 是在应用商店的专用内存范围内的虚拟地址。 参数 4 是 MemoryDescriptorList。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8884</p></td>
<td align="left"><p>(仅在 Windows 7 中)。 已假定具有相同的页面优先级值的两个页面在待机列表不是，实际上，有相同的页面优先级值。 在参数 4 中捕获的不同值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8888</p>
<p>0x8889</p></td>
<td align="left"><p>内部内存管理结构已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x888A</p></td>
<td align="left"><p>内部内存管理结构 （可能 PTE 或 PFN） 已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9696</p></td>
<td align="left"><p>PFN （参数 2） 遇到带不再连接到其最高级别进程损坏链接。  这表示 PFN 结构中的损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15001</p></td>
<td align="left"><p>以前受保护的未保护内存的过程中出错。  这可以调用方会错误地调用 MmUnsecureVirtualMemory 错误进程上下文中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41201</p></td>
<td align="left"><p>查询的虚拟地址的过程中出现页框架 Number(PFN) 和当前的页表项 (PTE) 指针之间的不一致。 参数 2 是相应 PTE。 参数 3 是 PTE 内容和参数 4 是虚拟地址描述符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41283</p></td>
<td align="left"><p>在将 PTE 中编码的工作集索引已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41284</p></td>
<td align="left"><p>PTE 或工作集列表已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>调用方尝试释放无效池地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41785</p></td>
<td align="left"><p>工作集列表已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41287</p></td>
<td align="left"><p>保存工作集同步时出现非法页面错误。 参数 2 包含被引用的虚拟地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41790</p></td>
<td align="left"><p>页表页已损坏。 Windows 的 64 位版本，参数 2 包含损坏的页表页 PFN 的地址。 Windows 的 32 位版本，参数 2 包含指向使用 Pte 数的指针，参数 3 包含使用 Pte 数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41792</p></td>
<td align="left"><p>已检测到损坏的 PTE。 参数 2 包含 PTE 的地址。 参数 3/4 包含 PTE 低/高部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41793</p></td>
<td align="left"><p> 页表页已损坏。 参数 2 包含最后一个处理 PTE 的指针。 参数 3 包含找到的非零值 Pte 数。 参数 4 包含预期的页表中的非零值 Pte 数。</p><p>此内存参数已弃用，并在 Windows 10 版本 1803年之后将不再可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61940</p></td>
<td align="left"><p>PDE 已意外失效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61941</p></td>
<td align="left"><p>分页的层次结构已损坏。 参数 2 是导致错误的虚拟地址的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61946</p></td>
<td align="left"><p>正在创建 MDL 有缺陷。 这几乎总是意味着存在驱动程序调用<strong>MmProbeAndLockPages</strong>出现故障。 通常，驱动程序正在尝试创建编写 MDL 时要求它处理分页读取。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61948</p></td>
<td align="left"><p>在 I/O 空间区域的引用计数的递减，过程中无法找到其记帐节点。  通常，这意味着自变量范围永远不会锁定或已经解锁。  参数 2 为基础的 I/O 帧。 参数 3 是在区域中的页数，参数 4 是找不到的节点的特定 I/O 帧。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61949</p></td>
<td align="left"><p>IoPageFrameNode 为 null。 参数 2 是 PageFrameIndex。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6194A</p></td>
<td align="left"><p>递减引用计数在 I/O 空间物理页的正在取消映射时出错。 正在取消引用当前未引用的项。  参数 2 和 3 描述正在取消映射，调用方的 I/O 空间范围和参数 4 是 I/O 空间物理页预计将引用，但不是。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03030303</p></td>
<td align="left"><p>启动加载器已断开。 （此值仅适用于 Intel Itanium 计算机。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03030308</p></td>
<td align="left"><p>要删除 （或截断） 的范围正在使用由加载程序以便它不能安全地删除，因此系统必须发出停止代码。  参数 2 是 HighestPhysicalPage。</p></td>
</tr>
</tbody>
</table>


<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。 

运行[ **Windows 内存诊断**](https://social.technet.microsoft.com/wiki/contents/articles/29343.windows-10-technical-preview-running-windows-memory-diagnostics-tool.aspx)工具可能很有用，以排除任何类型的问题影响的物理内存模块。
