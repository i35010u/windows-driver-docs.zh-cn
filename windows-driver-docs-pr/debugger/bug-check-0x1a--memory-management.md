---
title: Bug 检查 0x1A MEMORY_MANAGEMENT
description: MEMORY_MANAGEMENT bug 检查的值为 0x0000001A。 这表明出现了严重的内存管理错误。
ms.assetid: 7d3ff54e-e61a-43fa-a378-fb8d32565586
keywords:
- Bug 检查 0x1A MEMORY_MANAGEMENT
- MEMORY_MANAGEMENT
ms.date: 02/04/2020
topic_type:
- apiref
api_name:
- MEMORY_MANAGEMENT
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: 86962e0d29df9fc1f7019c2cef24629c31f6fee7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534650"
---
# <a name="bug-check-0x1a-memory_management"></a>Bug 检查 0x1A：MEMORY\_MANAGEMENT

MEMORY\_MANAGEMENT bug 检查的值为 0x0000001A。 这表明出现了严重的内存管理错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="memory_management-parameters"></a>MEMORY\_MANAGEMENT 参数

参数 1 标识完全冲突。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">错误消息的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>分叉克隆块引用计数已损坏。 这种情况仅发生在已检查的 Windows 版本上。 Windows 10 版本 1803 之前的旧版 Windows 上提供已检查的版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x31</p></td>
<td align="left"><p>映像重新定位修复表或代码流已损坏。 这可能是硬件错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3f</p></td>
<td align="left"><p>inpage 操作失败，出现 CRC 错误。 参数 2 包含页面文件偏移量。 参数 3 包含页 CRC 值。 参数 4 包含预期的 CRC 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x403</p></td>
<td align="left"><p>页面表和 PFN 不同步。 这可能是硬件错误，尤其是在参数 3 和 4 仅相差一位的情况下。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x404</p></td>
<td align="left"><p>在删除系统页的过程中，页帧编号 (PFN) 和当前页表条目 (PTE) 指针之间存在不一致。 参数 2 是预期的 PTE。 参数 3 是 PTE 内容，参数 4 是 PFN 的 PTE。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x411</p></td>
<td align="left"><p>页表条目 (PTE) 已损坏。 参数 2 是 PTE 的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x777</p></td>
<td align="left"><p>调用方正在解锁当前未锁定的系统缓存地址。 （此地址可能从未映射过，或已解除锁定两次。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x778</p></td>
<td align="left"><p>系统正在使用最新系统缓存视图地址，而不是保留它。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x780</p>
<p>0x781</p></td>
<td align="left"><p>映射参数系统缓存视图的 PTE 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p><strong>MmGetSystemAddressForMdl*</strong> 的调用方试图将完全缓存的物理页映射为非缓存页。 此操作将导致硬件转换缓冲区条目出现冲突，因此被操作系统拒绝。 由于调用方在请求的 MDL 中指定了“bug check on failure”，因此在此实例中系统别无选择，只能发出 bug 检查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>调用方正在解锁当前未锁定的可分页部分。 （此部分可能从未锁定过，或已解除锁定两次。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1233</p></td>
<td align="left"><p>驱动程序试图映射未锁定的物理内存页。 这是非法的，因为页面的内容或属性可以随时更改。 这是进行映射调用的代码中的 bug。 参数 2 是驱动程序尝试映射的物理页的页帧编号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1234</p></td>
<td align="left"><p>调用方正在尝试锁定不存在的可分页部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1235</p></td>
<td align="left"><p>调用方尝试用无效映射保护 MDL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1236</p></td>
<td align="left"><p>调用方指定了包含未锁定（或无效）物理页的 MDL。 参数 2 包含指向 MDL 的指针。 参数 3 包含指向无效 PFN 的指针。 参数 4 包含无效的 PFN 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1240</p></td>
<td align="left"><p>调用方为非常驻虚拟地址范围生成 MDL 是非法的。 参数 2 是内存描述符列表 (MDL)，参数 3 是 PTE 指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1241</p></td>
<td align="left"><p>MDL 的虚拟地址在调用生成 MDL 的中途意外地异步取消映射。 参数 2 是 MDL，参数 3 是 PTE 指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3300</p></td>
<td align="left"><p>在执行写入操作的过程中，引用的虚拟地址被错误地标记为“copy on write”。 参数 2 是 FaultingAddress。  参数 3 是 PTE 内容。 参数 4表 示虚拟地址空间类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3451</p></td>
<td align="left"><p>已调出的内核线程堆栈的 PTE 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3453</p></td>
<td align="left"><p>由于引用未完成，无法删除已退出进程的所有页表页。  这通常表示进程的页表结构已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3470</p></td>
<td align="left"><p>缓存的内核堆栈在可用列表上时已损坏 - 此内存损坏表示调用堆栈可能遇到或引发了严重问题。 参数 2 是虚拟地址 (VA)，参数 3 是 VA Cookie。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4477</p></td>
<td align="left"><p>驱动程序尝试写入系统进程的用户空间中未分配的地址。 参数 2 包含尝试写入的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5003</p></td>
<td align="left"><p>工作集可用列表已损坏。 这可能是硬件错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5100</p></td>
<td align="left"><p>分配位图已损坏。 内存管理器即将覆盖已在使用的虚拟地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5200</p></td>
<td align="left"><p>可用池列表上的页已损坏。 这可能是由于驱动程序中的 write-after-free bug 或上一页的溢出造成的。 参数 2 包含可用池块的地址。 参数 4 包含预期位于该地址的值。 参数 3 包含找到的实际值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5305</p></td>
<td align="left"><p>调用方正在指定要释放的无效池地址（参数 2）。 参数 2 是正在计算的虚拟地址 (VA)，参数 3 是区域大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6001</p></td>
<td align="left"><p>内存存储组件的专用内存范围已损坏，导致无法访问它。 参数 2 是返回的状态。  参数 3 是存储的专用内存范围内的虚拟地址。 参数 4 是 MemoryDescriptorList。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8884</p><p>0x8885</p><p>0x8886</p><p>0x8887</p></td>
<td align="left"><p>（Windows 7 及更高版本）。 备用列表中的两个页面本来应该具有相同的页面优先级值，但实际上它们没有相同的页面优先级值。 参数 4 中捕获了不同的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8888</p><p>0x8889</p></td>
<td align="left"><p>内部内存管理结构已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x888A</p></td>
<td align="left"><p>内部内存管理结构（可能是 PTE 或 PFN）已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9696</p></td>
<td align="left"><p>遇到 PFN （参数 2），损坏的链接不再连接到其顶层进程。  这表示 PFN 结构中的损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15000</p></td>
<td align="left"><p>调用方提供了错误的地址，或者正在错误的进程上下文中调用此例程。  这两者都是非法的，因为我们无法取消保护由于此错误而找不到的范围。 参数 2 是要评估的虚拟地址 (VA)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x15001</p></td>
<td align="left"><p>在取消保护以前已保护的内存的过程中发生错误。  如果调用方误在错误的进程上下文中调用 MmUnsecureVirtualMemory，则可能会发生这种情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41201</p></td>
<td align="left"><p>在查询虚拟地址的过程中，页帧编号 (PFN) 和当前页表条目 (PTE) 指针之间存在不一致。 参数 2 是对应的 PTE。 参数 3 是 PTE 内容，参数 4 是虚拟地址描述符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41202</p></td>
<td align="left"><p>在确定非零 PTE 的页保护的过程中，已确定 PTE 已损坏。  参数 2 是 PTE 指针，参数 3 是 PTE 内容，参数 4 是虚拟地址描述符 (VAD)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41283</p></td>
<td align="left"><p>PTE 中编码的工作集索引已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41284</p></td>
<td align="left"><p>PTE 或工作集列表已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>调用方试图释放无效的池地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41785</p></td>
<td align="left"><p>工作集列表已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41287</p></td>
<td align="left"><p>保持工作集同步时出现非法页错误。 参数 2 包含引用的虚拟地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41790</p></td>
<td align="left"><p>页表页已损坏。 在 64 位版本的 Windows 上，参数 2 包含损坏页表页的 PFN 地址。 在 32 位版本的 Windows 上，参数 2 包含指向已使用 PTE 数的指针，参数 3 包含已使用 PTE 数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41792</p></td>
<td align="left"><p>检测到损坏的 PTE。 参数 2 包含 PTE 的地址。 参数 3/4 包含 PTE 的低/高部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41793</p></td>
<td align="left"><p> 页表页已损坏。 参数 2 包含指向上次处理的 PTE 的指针。 参数 3 包含找到的非零 PTE 数。 参数 4 包含页表中预期数量的非零 PTE。</p><p>此内存参数已弃用，在 Windows 10 版本 1803 后不再可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61940</p></td>
<td align="left"><p>PDE 意外失效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61941</p></td>
<td align="left"><p>分页层次结构已损坏。 参数 2 是指向导致故障的虚拟地址的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61946</p></td>
<td align="left"><p>正在创建的 MDL 有缺陷。 这几乎始终意味着调用 <strong>MmProbeAndLockPages</strong> 的驱动程序有错误。 通常，当请求驱动程序处理分页读取时，它会尝试创建“写入 MDL”。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x61948</p></td>
<td align="left"><p>在递减 I/O 空间区域的引用计数的过程中，找不到其计帐节点。  通常这意味着参数范围从未锁定或已解锁。  参数 2 是基本 I/O 帧。 参数 3 是区域中的页数，参数 4 是找不到其节点的特定 I/O 帧。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x61949</p></td>
<td align="left"><p>IoPageFrameNode 为 null。 参数 2 为 PageFrameIndex。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6194A</p></td>
<td align="left"><p>减小正在取消映射的 I/O 空间物理页上的引用计数时出错。 将取消引用当前未引用的条目。  参数 2 和 3 描述正在取消映射的调用方的 I/O 空间范围，参数 4 是 I/O 空间物理页，预期要引用，但未引用。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03030303</p></td>
<td align="left"><p>启动加载器已损坏。 （此值仅适用于 Intel Itanium 计算机。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03030308</p></td>
<td align="left"><p>加载器正在使用要删除（或截断）的范围，因此无法安全删除该范围，系统必须发出停止代码。  参数 2 为 HighestPhysicalPage。</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>解决方法
----------

[!analyze](-analyze.md) 调试扩展显示有关 bug 检查的信息，并有助于确定根本原因  。

运行 Windows 内存诊断工具对于排除任何影响物理内存模块的问题也很有用。
