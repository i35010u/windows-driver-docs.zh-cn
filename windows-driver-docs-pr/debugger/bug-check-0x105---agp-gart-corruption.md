---
title: Bug 检查 0x105 AGP_GART_CORRUPTION
description: AGP_GART_CORRUPTION bug 检查的值为0x00000105。 这表明 (GART) 的图形口径重新映射表已损坏。
keywords:
- Bug 检查 0x105 AGP_GART_CORRUPTION
- AGP_GART_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_GART_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b06cc0484648292c11827bf4ae9ee8a84c3fe7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790081"
---
# <a name="bug-check-0x105-agp_gart_corruption"></a>Bug 检查0x105： AGP \_ GART \_ 损坏


AGP \_ GART \_ 损坏 bug 检查的值为0x00000105。 这表明 (GART) 的图形口径重新映射表已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="agp_gart_corruption-parameters"></a>AGP \_ GART \_ 损坏参数


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
<td align="left"><p>1</p></td>
<td align="left"><p>GART 的基址 (虚拟) </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>发生损坏的 GART 中的偏移量</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>GART 缓存的基址 (虚拟)  (GART 的副本) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此 bug 检查通常是由驱动程序 (DMA) 不当引起的直接内存访问。

<a name="resolution"></a>解决方法
----------

为任何未签名的驱动程序启用驱动程序验证程序。 删除它们或逐个将其禁用，直到识别到 erring 驱动程序。

 

 




