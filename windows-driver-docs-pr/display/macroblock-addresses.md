---
title: 宏块地址
description: 宏块地址
keywords:
- macroblocks WDK DirectX VA，地址
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 906d539130b24b55a652d03b10106016de53f8d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832389"
---
# <a name="macroblock-addresses"></a>宏块地址


## <span id="ddk_macroblock_addresses_gg"></span><span id="DDK_MACROBLOCK_ADDRESSES_GG"></span>


宏块地址是图片内宏块的位置（以光栅扫描顺序排列）。 图片中的宏块的水平和垂直位置是使用图片的指定宽度和高度（由 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **wPicWidthInMBminus1** 和 **wPicHeightInMBminus1** 成员定义）来确定的。 下面是宏块地址的一些示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏块</th>
<th align="left">地址</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>左上角</p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p>右上方</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>左下角</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x (<strong>wPicWidthInMBminus1</strong> + 1)</p></td>
</tr>
<tr class="even">
<td align="left"><p>右下</p></td>
<td align="left"><p> (<strong>wPicHeightInMBminus1</strong> + 1) x (<strong>wPicWidthInMBminus1</strong> + 1) - 1</p></td>
</tr>
</tbody>
</table>

 

 

