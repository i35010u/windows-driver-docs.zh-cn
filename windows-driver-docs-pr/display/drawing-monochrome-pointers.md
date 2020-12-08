---
title: 绘制单色指针
description: 绘制单色指针
keywords:
- 绘图指针 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，指针
- 指针 WDK Windows 2000 显示
- 单色指针 WDK Windows 2000 显示
- 黑白指针 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 514c346065b9e44373b9a3245e72e37bf5e23367
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809183"
---
# <a name="drawing-monochrome-pointers"></a>绘制单色指针


## <span id="ddk_drawing_monochrome_pointers_gg"></span><span id="DDK_DRAWING_MONOCHROME_POINTERS_GG"></span>


单色位图由两部分组成：第一个部分定义指针的和掩码;第二个定义 XOR 掩码。 这些掩码一起为指针图像的每个像素提供两位信息。 下表说明了和和 XOR 掩码中指定的值的显示结果。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">和掩码值</th>
<th align="left">XOR 掩码值</th>
<th align="left">显示结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>像素为黑色</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>像素为白色</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>像素 (透明) 不变</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>像素颜色反转</p></td>
</tr>
</tbody>
</table>

 

此位图定义和使用情况提供了一个黑白图像，同时为构成指针的像素的透明度和反转提供支持。

 

 





