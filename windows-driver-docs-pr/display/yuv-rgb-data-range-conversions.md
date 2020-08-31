---
title: YUV-RGB 数据范围转换
ms.assetid: 0A439686-0BAE-4E4D-AA23-06A6EF72C4B3
description: 输入数据范围对预期的视频转换行为的影响
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f278d457924c5af25d56ee2fd4a340ed0819a4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063430"
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
<th align="left">输入</th>
<th align="left">输入</th>
<th align="left">输入</th>
<th align="left">输入</th>
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
<td align="left">低</td>
<td align="left">RGB</td>
<td align="left">低</td>
<td align="left">format</td>
<td align="left">data</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left">range</td>
<td align="left"></td>
<td align="left">range</td>
<td align="left">range</td>
<td align="left">range</td>
<td align="left">range</td>
<td align="left"></td>
<td align="left">range</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">空值</td>
<td align="left">2</td>
<td align="left">空值</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">无</td>
</tr>
<tr class="even">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">空值</td>
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
<td align="left">空值</td>
<td align="left">1</td>
<td align="left">不适用</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">缩放</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">空值</td>
<td align="left">2</td>
<td align="left">空值</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">缩放</td>
</tr>
<tr class="odd">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">空值</td>
<td align="left">空值</td>
<td align="left">1</td>
<td align="left">YUV</td>
<td align="left">16-235</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">RGB</td>
<td align="left">0</td>
<td align="left">空值</td>
<td align="left">空值</td>
<td align="left">2</td>
<td align="left">YUV</td>
<td align="left">0-255</td>
<td align="left">RGBtoYUV</td>
</tr>
<tr class="odd">
<td align="left">16-235</td>
<td align="left">YUV</td>
<td align="left">空值</td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left">空值</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
<tr class="even">
<td align="left">0-255</td>
<td align="left">YUV</td>
<td align="left">空值</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left">空值</td>
<td align="left">RGB</td>
<td align="left">0-255</td>
<td align="left">YUVtoRGB</td>
</tr>
</tbody>
</table>

 

在这种情况下，"名义范围" 是 [**DXVAHDDDI \_ 标称 \_ 范围**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_nominal_range) 枚举中的常量值。

有关 YUV 格式范围的定义，请参阅 [Windows 8.1 中的 yuv 格式范围](yuv-format-ranges.md) 。

 

