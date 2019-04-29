---
title: 宏块地址
description: 宏块地址
ms.assetid: f04c5462-db7c-4917-b8ef-22a630c82994
keywords:
- 宏块 WDK DirectX va，因此地址
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e609bb2729ffb292677697735cd821b790681efc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375376"
---
# <a name="macroblock-addresses"></a>宏块地址


## <span id="ddk_macroblock_addresses_gg"></span><span id="DDK_MACROBLOCK_ADDRESSES_GG"></span>


宏块地址是在图片中的光栅扫描顺序宏块的位置。 水平和垂直位置宏块的图中确定使用指定的宽度和高度图中，由定义的宏块地址**wPicWidthInMBminus1**和**wPicHeightInMBminus1**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构。 以下是一些示例宏块地址。

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
<td align="left"><p>top-left</p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p>top-right</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>lower-left</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x (<strong>wPicWidthInMBminus1</strong> + 1)</p></td>
</tr>
<tr class="even">
<td align="left"><p>lower-right</p></td>
<td align="left"><p>(<strong>wPicHeightInMBminus1</strong> + 1) x (<strong>wPicWidthInMBminus1</strong> + 1) - 1</p></td>
</tr>
</tbody>
</table>

 

 

 





