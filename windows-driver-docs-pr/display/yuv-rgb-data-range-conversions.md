---
title: YUV-RGB 数据范围转换
ms.assetid: 0A439686-0BAE-4E4D-AA23-06A6EF72C4B3
description: 预期的视频转换行为对输入的数据范围的影响
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53895cd9c67883985ae59ad15f4ba019fe95c816
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372005"
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
<td align="left">data</td>
<td align="left">format</td>
<td align="left">RGB</td>
<td align="left">名义</td>
<td align="left">RGB</td>
<td align="left">名义</td>
<td align="left">format</td>
<td align="left">data</td>
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
<td align="left">不可用</td>
<td align="left">2</td>
<td align="left">不可用</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">不可用</td>
<td align="left">1</td>
<td align="left">不可用</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">不可用</td>
<td align="left">1</td>
<td align="left">不可用</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">比例</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">不可用</td>
<td align="left">2</td>
<td align="left">不可用</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">比例</td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">不可用</td>
<td align="left">不可用</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">不可用</td>
<td align="left">不可用</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">不可用</td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left">不可用</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">不可用</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left">不可用</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
</tbody>
</table>

 

在这种情况下的"名义范围"是中的常量值[ **DXVAHDDDI\_名义\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_dxvahdddi_nominal_range)枚举。

请参阅[YUV 格式范围在 Windows 8.1 中](yuv-format-ranges.md)定义 YUV 格式显示范围。

 

 





