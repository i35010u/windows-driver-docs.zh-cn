---
title: YUV RGB 数据范围转换
ms.assetid: 0A439686-0BAE-4E4D-AA23-06A6EF72C4B3
description: 预期的视频转换行为对输入的数据范围的影响
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6022ff07872ee15099e8d4f96674eed88ec540b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542960"
---
# <a name="span-iddisplayyuv-rgbdatarangeconversionsspanyuv-rgb-data-range-conversions"></a><span id="display.yuv-rgb_data_range_conversions"></span>YUV RGB 数据范围转换


如果你想要从 RGB 或 YUV YUV 或 RGB 输出的输入转换，预期的行为取决于输入的数据范围：

<table>
<colgroup>
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Input</th>
<th align="left">Input</th>
<th align="left">Input</th>
<th align="left">Input</th>
<th align="left">输出</th>
<th align="left">输出</th>
<th align="left">输出</th>
<th align="left">输出</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">数据</td>
<td align="left">format</td>
<td align="left">RGB</td>
<td align="left">名义</td>
<td align="left">RGB</td>
<td align="left">名义</td>
<td align="left">format</td>
<td align="left">数据</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">范围</td>
<td align="left"></td>
<td align="left">范围</td>
<td align="left">范围</td>
<td align="left">范围</td>
<td align="left">范围</td>
<td align="left"></td>
<td align="left">范围</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">不适用</td>
<td align="left">2</td>
<td align="left">不适用</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">不适用</td>
<td align="left">1</td>
<td align="left">不适用</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">不适用</td>
<td align="left">1</td>
<td align="left">不适用</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">比例</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">不适用</td>
<td align="left">2</td>
<td align="left">不适用</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">比例</td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">不适用</td>
<td align="left">不适用</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">不适用</td>
<td align="left">不适用</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">不适用</td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left">不适用</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">不适用</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left">不适用</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
</tbody>
</table>

 

在这种情况下的"名义范围"是中的常量值[ **DXVAHDDDI\_名义\_范围**](https://msdn.microsoft.com/library/windows/hardware/dn265432)枚举。

请参阅[YUV 格式范围在 Windows 8.1 中](yuv-format-ranges.md)定义 YUV 格式显示范围。

 

 





