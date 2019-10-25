---
title: YUV-RGB 数据范围转换
ms.assetid: 0A439686-0BAE-4E4D-AA23-06A6EF72C4B3
description: 输入数据范围对预期的视频转换行为的影响
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d39a7325bdab737e251096e4043e6cfd31cdb82a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829123"
---
# <a name="span-iddisplayyuv-rgb_data_range_conversionsspanyuv-rgb-data-range-conversions"></a><span id="display.yuv-rgb_data_range_conversions"></span>YUV-RGB 数据范围转换


如果要从 RGB 或 YUV 输入转换到 YUV 或 RGB 输出，预期的行为取决于输入数据范围：

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
<td align="left">低</td>
<td align="left">RGB</td>
<td align="left">低</td>
<td align="left">format</td>
<td align="left">数据</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">内</td>
<td align="left"></td>
<td align="left">内</td>
<td align="left">内</td>
<td align="left">内</td>
<td align="left">内</td>
<td align="left"></td>
<td align="left">内</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">N/A</td>
<td align="left">2</td>
<td align="left">N/A</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">N/A</td>
<td align="left">1</td>
<td align="left">N/A</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">无</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">N/A</td>
<td align="left">1</td>
<td align="left">N/A</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">比例</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">N/A</td>
<td align="left">2</td>
<td align="left">N/A</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">比例</td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">N/A</td>
<td align="left">N/A</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">N/A</td>
<td align="left">N/A</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">N/A</td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left">N/A</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">N/A</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left">N/A</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
</tbody>
</table>

 

在这种情况下，"名义范围" 是[**DXVAHDDDI\_公称\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_nominal_range)枚举的常量值。

有关 YUV 格式范围的定义，请参阅[Windows 8.1 中的 yuv 格式范围](yuv-format-ranges.md)。

 

 





