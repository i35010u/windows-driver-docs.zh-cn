---
title: Bug 检查 0xDA SYSTEM_PTE_MISUSE
description: SYSTEM_PTE_MISUSE bug 检查的值为0x000000DA。 这表示已使用了一种不正确的方法来使用页表项（PTE）例程。
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
ms.openlocfilehash: 023727b030c7644f39bac5bf7173fcfe324a9a7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827363"
---
# <a name="bug-check-0xda-system_pte_misuse"></a>Bug 检查0xDA：\_误用系统\_PTE


系统\_PTE\_误用 bug 检查的值为0x000000DA。 这表示已使用了一种不正确的方法来使用页表项（PTE）例程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="system_pte_misuse-parameters"></a>系统\_PTE\_误用参数


参数1指示违规类型。 其他参数的意义取决于参数1的值。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>内部锁跟踪结构的地址</p></td>
<td align="left"><p>内存描述符列表的地址</p></td>
<td align="left"><p>重复内部锁跟踪结构的地址</p></td>
<td align="left"><p>要释放的映射是重复的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>内部锁跟踪结构的地址</p></td>
<td align="left"><p>系统预期会释放的映射数</p></td>
<td align="left"><p>驱动程序请求释放的映射数</p></td>
<td align="left"><p>正在释放的映射数不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>找到的第一个内部跟踪结构的地址</p></td>
<td align="left"><p>系统预期要释放的映射地址</p></td>
<td align="left"><p>驱动程序请求释放的映射地址</p></td>
<td align="left"><p>正在释放的映射地址不正确。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>内部锁跟踪结构的地址</p></td>
<td align="left"><p>系统预期的页面帧号应在 MDL 中首先</p></td>
<td align="left"><p>当前在 MDL 中的第一页的帧号</p></td>
<td align="left"><p>映射 MDL 后，映射 MDL 的第一页发生了更改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>找到的第一个内部跟踪结构的地址</p></td>
<td align="left"><p>系统预期要释放的虚拟地址</p></td>
<td align="left"><p>驱动程序请求释放的虚拟地址</p></td>
<td align="left"><p>自映射 MDL 后，要释放的 MDL 中的启动虚拟地址已发生更改。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>驱动程序指定的 MDL</p></td>
<td align="left"><p>驱动程序指定的虚拟地址</p></td>
<td align="left"><p>要释放的映射数（由驱动程序指定）</p></td>
<td align="left"><p>正在释放的 MDL 从未（或当前未）映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>映射的数目</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>（仅限 Windows 2000）映射范围为双精度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>调用方正在释放的映射数</p></td>
<td align="left"><p>系统认为应释放的映射数</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方请求的映射数量不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>调用方正在释放的映射数</p></td>
<td align="left"><p>系统认为已经免费的映射索引</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方请求释放多个映射，但至少有一个映射未分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p><strong>1：</strong>该驱动程序在 MDL 中请求了 "失败时 bug 检查"。</p>
<p><strong>0：</strong>该驱动程序未请求在 MDL 中出现 "失败时 bug 检查"。</p></td>
<td align="left"><p>调用方分配的映射数</p></td>
<td align="left"><p>请求的映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方请求分配零个映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>损坏的映射</p></td>
<td align="left"><p>调用方分配的映射数</p></td>
<td align="left"><p>请求的映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）此分配时，映射列表已损坏。 损坏的映射位于可能的最小映射地址下面。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>损坏的映射</p></td>
<td align="left"><p>调用方分配的映射数</p></td>
<td align="left"><p>请求的映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）此分配时，映射列表已损坏。 损坏的映射位于可能的最小映射地址之上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>调用方正在释放的映射数</p></td>
<td align="left"><p>映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方正在尝试释放零映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>初始映射</p></td>
<td align="left"><p>调用方正在释放的映射数</p></td>
<td align="left"><p>映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方正在尝试释放映射，但保护映射已被覆盖。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>不存在的映射</p></td>
<td align="left"><p>调用方尝试释放的映射数</p></td>
<td align="left"><p>正在释放的映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方正在尝试释放不存在的映射。 不存在的映射位于可能的最小映射地址下面。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>不存在的映射</p></td>
<td align="left"><p>调用方尝试释放的映射数</p></td>
<td align="left"><p>正在释放的映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方正在尝试释放不存在的映射。 不存在的映射位于可能的最高映射地址之上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>不存在的映射</p></td>
<td align="left"><p>调用方尝试释放的映射数</p></td>
<td align="left"><p>正在释放的映射池的类型</p></td>
<td align="left"><p>（仅限 Windows 2000）调用方正在尝试释放不存在的映射。 映射地址空间的基础上不存在的映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>请求的映射数</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>调用此例程的调用方的例程的地址</p></td>
<td align="left"><p> 调用方请求了0个映射。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>所有者的标识标记</p></td>
<td align="left"><p> 调用方正在尝试释放其不拥有的映射地址范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方尝试释放的映射地址空间明显为空。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x103</p></td>
<td align="left"><p>无效映射的地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>映射地址空间中的映射数</p></td>
<td align="left"><p>调用方尝试释放的映射地址空间仍保留。 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping" data-raw-source="[MmUnmapReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping)">MmUnmapReservedMapping</a></strong></p>
<p>必须在<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreemappingaddress" data-raw-source="[MmFreeMappingAddress](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreemappingaddress)">MmFreeMappingAddress</a></strong>之前调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x104</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>所有者的标识标记</p></td>
<td align="left"><p>调用方尝试将 MDL 映射到其不拥有的映射地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x105</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方正在尝试将 MDL 映射到无效的映射地址空间。 调用方很可能指定了无效的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x107</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>非空映射的地址</p></td>
<td align="left"><p>最后一个映射地址</p></td>
<td align="left"><p>调用方尝试将 MDL 映射到未正确保留的映射地址空间。 调用方应在调用<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpageswithreservedmapping" data-raw-source="[MmMapLockedPagesWithReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpageswithreservedmapping)">MmMapLockedPagesWithReservedMapping</a></strong>之前调用<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping" data-raw-source="[MmUnmapReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping)">MmUnmapReservedMapping</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x108</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>所有者的标识标记</p></td>
<td align="left"><p>调用方正在尝试取消映射它不拥有的已锁定映射地址空间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x109</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方正在尝试取消映射明显为空的已锁定虚拟地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10A</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>锁定映射地址空间中的映射数</p></td>
<td align="left"><p>映射到未映射的数目</p></td>
<td align="left"><p>调用方正在尝试取消映射超出锁定映射地址空间中实际存在的映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10B</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>映射到未映射的数目</p></td>
<td align="left"><p>调用方正在尝试取消映射当前未映射的已锁定虚拟地址空间的一部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10C</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方的标识标记</p></td>
<td align="left"><p>映射到未映射的数目</p></td>
<td align="left"><p>调用方不会取消整个已锁定映射地址空间的映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试保留不包含映射的映射地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x201</p>
<p>0x202</p></td>
<td align="left"><p>要保留的第一个映射地址</p></td>
<td align="left"><p>已保留的映射的地址</p></td>
<td align="left"><p>要保留的映射的数目</p></td>
<td align="left"><p>调用方尝试保留的映射之一已被保留。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x300</p></td>
<td align="left"><p>要释放的第一个映射地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方正在尝试释放不包含映射的映射地址空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x301</p></td>
<td align="left"><p>映射的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方正在尝试释放不允许其发布的映射。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x302</p></td>
<td align="left"><p>调用方尝试释放的地址。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方正在尝试释放当前未映射的系统地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x303</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>要发布的映射数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方正在尝试释放未保留的映射地址范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x304</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>要发布的映射数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方正在尝试释放在不同分配中间开始的映射地址范围。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x305</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>调用方尝试释放的映射数</p></td>
<td align="left"><p>应释放的映射数</p></td>
<td align="left"><p>调用方尝试释放错误的映射数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x306</p></td>
<td align="left"><p>第一个映射地址</p></td>
<td align="left"><p>免费映射地址</p></td>
<td align="left"><p>要发布的映射数</p></td>
<td align="left"><p>调用方正在尝试释放的一个映射已经免费用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p>I/o 空间映射的基址</p></td>
<td align="left"><p>要释放的页数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>调用方尝试释放系统无法识别的 i/o 空间映射。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

错误由参数1的值指示。

堆栈跟踪将标识导致错误的驱动程序。

 

 




