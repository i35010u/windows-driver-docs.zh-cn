---
title: 宏块地址
description: 宏块地址
ms.assetid: f04c5462-db7c-4917-b8ef-22a630c82994
keywords:
- macroblocks WDK DirectX VA，地址
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e25691e4dd9255ba11ff8aba10d2f5acbc6bea1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840593"
---
# <a name="macroblock-addresses"></a>宏块地址


## <span id="ddk_macroblock_addresses_gg"></span><span id="DDK_MACROBLOCK_ADDRESSES_GG"></span>


宏块地址是图片内宏块的位置（以光栅扫描顺序排列）。 图片中的宏块的水平和垂直位置是使用指定图片的宽度和高度（由**wPicWidthInMBminus1**和**wPicHeightInMBminus1**成员定义）从宏块地址确定的。[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构。 下面是宏块地址的一些示例。

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
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p>右上方</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>左下角</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x （<strong>wPicWidthInMBminus1</strong> + 1)</p></td>
</tr>
<tr class="even">
<td align="left"><p>右下</p></td>
<td align="left"><p>（<strong>wPicHeightInMBminus1</strong> + 1) x （<strong>wPicWidthInMBminus1</strong> + 1) - 1</p></td>
</tr>
</tbody>
</table>

 

 

 





