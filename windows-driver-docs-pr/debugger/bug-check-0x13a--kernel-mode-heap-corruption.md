---
title: Bug 检查 0x13A KERNEL_MODE_HEAP_CORRUPTION
description: KERNEL_MODE_HEAP_CORRUPTION bug 检查具有 0x0000013A 值。 这表示，内核模式堆管理器检测到损坏堆中。
ms.assetid: 806669B3-B811-462A-A3B6-2F583BF0E19A
keywords:
- Bug 检查 0x13A KERNEL_MODE_HEAP_CORRUPTION
- KERNEL_MODE_HEAP_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_MODE_HEAP_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66c9fd99d3c6b40cddb340c686bf28bb845b5687
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238532"
---
# <a name="bug-check-0x13a-kernelmodeheapcorruption"></a>Bug 检查 0x13A：内核\_模式下\_堆\_损坏


内核\_模式下\_堆\_损坏错误检查的值为 0x0000013A。 这表示，内核模式堆管理器检测到损坏堆中。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="kernelmodeheapcorruption-parameters"></a>内核\_模式下\_堆\_损坏参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>检测到损坏的类型</p>
0x3:检测到损坏条目标头。
0x4:检测到多个损坏条目标头。
0x5:检测到损坏条目标头中分配大量的。
0x6:与缓冲区溢出一致的功能检测到损坏。
0x7:缓冲区不足与一致的功能检测到损坏。
0x8:可用块传递到所适用的繁忙的块的操作。
0x9:当前操作指定的参数无效。
0xA:与使用后免费错误一致的功能检测到损坏。
0xB:为当前操作指定了错误的堆。
0xC:检测到损坏的空闲列表。
0xD:堆以外空闲列表的列表中检测到列表损坏。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">报告损坏堆的地址</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">地址损坏检测</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




