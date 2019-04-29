---
title: Bug 检查 0xDA SYSTEM_PTE_MISUSE
description: SYSTEM_PTE_MISUSE bug 检查具有 0x000000DA 值。 这表示一种不正确的方法中已使用的页表项 (PTE) 例程。
ms.assetid: a9a9f3e9-39b7-4e4a-a326-2f510e0aaa99
keywords:
- Bug 检查 0xDA SYSTEM_PTE_MISUSE
- SYSTEM_PTE_MISUSE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_PTE_MISUSE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16ae75a5de50453400e8463990805b1c82d98118
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371727"
---
# <a name="bug-check-0xda-systemptemisuse"></a>Bug 检查 0xDA：系统\_PTE\_滥用


系统\_PTE\_滥用 bug 检查的值为 0x000000DA。 这表示一种不正确的方法中已使用的页表项 (PTE) 例程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="systemptemisuse-parameters"></a>系统\_PTE\_误用参数


参数 1 指示冲突的类型。 其他参数的含义取决于参数 1 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>跟踪结构内部锁的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>跟踪结构重复内部锁的地址</p></td>
<td align="left"><p>要释放的映射是重复项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>跟踪结构内部锁的地址</p></td>
<td align="left"><p>系统需要释放的映射的数量</p></td>
<td align="left"><p>该驱动程序正在请求要释放的映射的数量</p></td>
<td align="left"><p>要释放的映射的数量不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>找到的第一个内部跟踪结构的地址</p></td>
<td align="left"><p>系统要求以释放映射地址</p></td>
<td align="left"><p>请求驱动程序以释放映射地址</p></td>
<td align="left"><p>要释放的映射地址不正确。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>跟踪结构内部锁的地址</p></td>
<td align="left"><p>系统预期在帧页码应为 MDL 中的第一行</p></td>
<td align="left"><p>MDL 中的第一次当前帧页码</p></td>
<td align="left"><p>由于 MDL 已映射已更改映射 MDL 的第一页。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>找到的第一个内部跟踪结构的地址</p></td>
<td align="left"><p>系统要求以释放虚拟地址</p></td>
<td align="left"><p>请求驱动程序以释放虚拟地址</p></td>
<td align="left"><p>由于 MDL 已映射已更改中释放 MDL 起始虚拟地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>指定驱动程序 MDL</p></td>
<td align="left"><p>指定驱动程序的虚拟地址</p></td>
<td align="left"><p>若要释放的映射的数量 （由驱动程序指定）</p></td>
<td align="left"><p>正在释放 MDL 从来都不 （或不是当前） 映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>映射的数量</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>(仅适用于 Windows 2000)映射范围的双分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>释放调用方的映射的数量</p></td>
<td align="left"><p>应释放的系统认为的映射数</p></td>
<td align="left"><p>(仅适用于 Windows 2000)要求调用方免费的数目不正确的映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>释放调用方的映射的数量</p></td>
<td align="left"><p>系统认为映射索引已可用</p></td>
<td align="left"><p>(仅适用于 Windows 2000)调用方要求以释放多个映射，但至少一个未分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p><strong>1:</strong>该驱动程序请求的"bug 检查失败时"MDL 中。</p>
<p><strong>0:</strong>该驱动程序未请求"bug 检查失败时"MDL 中。</p></td>
<td align="left"><p>调用方分配的映射的数量</p></td>
<td align="left"><p>映射池请求的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)要求调用方分配零个映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>损坏的映射</p></td>
<td align="left"><p>调用方分配的映射的数量</p></td>
<td align="left"><p>映射池请求的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)在这种分配时，映射列表已损坏。 损坏的映射位于下面的最低可能的映射地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>损坏的映射</p></td>
<td align="left"><p>调用方分配的映射的数量</p></td>
<td align="left"><p>映射池请求的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)在这种分配时，映射列表已损坏。 上面的最低可能的映射地址位于已损坏的映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>释放调用方的映射的数量</p></td>
<td align="left"><p>映射池的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)调用方尝试释放零个映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>释放调用方的映射的数量</p></td>
<td align="left"><p>映射池的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)调用方尝试释放映射，但映射的防护已被覆盖。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>不存在映射</p></td>
<td align="left"><p>调用方尝试释放的映射的数量</p></td>
<td align="left"><p>要释放的映射池的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)调用方尝试释放不存在映射。 不存在映射位于下面的最低可能的映射地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>不存在映射</p></td>
<td align="left"><p>调用方尝试释放的映射的数量</p></td>
<td align="left"><p>要释放的映射池的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)调用方尝试释放不存在映射。 不存在映射位于上方的最高的可能的映射地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>不存在映射</p></td>
<td align="left"><p>调用方尝试释放的映射的数量</p></td>
<td align="left"><p>要释放的映射池的类型</p></td>
<td align="left"><p>(仅适用于 Windows 2000)调用方尝试释放不存在映射。 不存在映射是映射地址空间的基础。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>所请求的映射的数量</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>调用此例程的调用方的例程的地址</p></td>
<td align="left"><p> 调用方请求的 0 的映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>所有者的标识标记</p></td>
<td align="left"><p> 调用方尝试释放它没有自己的映射地址范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方尝试释放的映射地址空间为显然空。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x103</p></td>
<td align="left"><p>无效的映射的地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>映射地址空间中的映射数</p></td>
<td align="left"><p>调用方尝试释放映射地址空间是仍保留。 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff556392" data-raw-source="[MmUnmapReservedMapping](https://msdn.microsoft.com/library/windows/hardware/ff556392)">MmUnmapReservedMapping</a></strong></p>
<p>前必须调用 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff554512" data-raw-source="[MmFreeMappingAddress](https://msdn.microsoft.com/library/windows/hardware/ff554512)">MmFreeMappingAddress</a></strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x104</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>所有者的标识标记</p></td>
<td align="left"><p>调用方尝试将 MDL 映射到不拥有对映射地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x105</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方尝试将 MDL 映射到无效的映射地址空间。 调用方很可能已指定了无效的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x107</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>非空映射的地址</p></td>
<td align="left"><p>最后一个映射地址</p></td>
<td align="left"><p>调用方尝试将 MDL 映射到不正确地保留映射地址空间。 调用方应具有名为<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff556392" data-raw-source="[MmUnmapReservedMapping](https://msdn.microsoft.com/library/windows/hardware/ff556392)">MmUnmapReservedMapping</a></strong>之前调用 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff554640" data-raw-source="[MmMapLockedPagesWithReservedMapping](https://msdn.microsoft.com/library/windows/hardware/ff554640)">MmMapLockedPagesWithReservedMapping</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x108</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>所有者的标识标记</p></td>
<td align="left"><p>调用方尝试取消映射不拥有锁定的映射地址空间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x109</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方尝试取消映射为显然空锁定的虚拟地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10A</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>锁定的映射地址空间中的映射数</p></td>
<td align="left"><p>若要取消映射的映射的数量</p></td>
<td align="left"><p>调用方尝试取消映射多于实际存在的锁定的映射地址空间中的多个映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10B</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>若要取消映射的映射的数量</p></td>
<td align="left"><p>调用方尝试取消当前未映射的锁定的虚拟地址空间的一部分的映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10C</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>若要取消映射的映射的数量</p></td>
<td align="left"><p>调用方不取消映射整个锁定的映射地址空间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试保留包含没有映射的映射地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x201</p>
<p>0x202</p></td>
<td align="left"><p>要保留的第一个映射地址</p></td>
<td align="left"><p>已保留的映射的地址</p></td>
<td align="left"><p>若要保留的映射的数量</p></td>
<td align="left"><p>调用方尝试保留的映射之一已保留。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x300</p></td>
<td align="left"><p>要发布的第一个映射地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试释放不包含任何映射映射地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x301</p></td>
<td align="left"><p>映射的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试释放不允许发布的映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x302</p></td>
<td align="left"><p>调用方尝试释放地址。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方尝试释放当前未映射的系统地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x303</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>若要释放的映射的数量</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试释放未保留的映射地址范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x304</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>若要释放的映射的数量</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试释放不同的分配的中间开始映射地址范围。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x305</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方尝试释放的映射的数量</p></td>
<td align="left"><p>应释放的映射的数量</p></td>
<td align="left"><p>调用方尝试释放映射数目不正确。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x306</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>免费映射地址</p></td>
<td align="left"><p>若要释放的映射的数量</p></td>
<td align="left"><p>其中一个调用方尝试释放的映射已可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p>基址的 I/O 空间映射</p></td>
<td align="left"><p>要释放的页面数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试释放系统并不知道的 I/O 空间映射。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

参数 1 的值指示错误。

堆栈跟踪将标识导致错误的驱动程序。

 

 




