---
title: GDI 色彩空间转换
description: GDI 色彩空间转换
keywords:
- surface 协商 WDK GDI，颜色空间转换
- 颜色通道 WDK GDI
- 颜色空间转换 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19080c64474d5fba7cde883934172e60511db954
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806385"
---
# <a name="gdi-color-space-conversions"></a>GDI 色彩空间转换


## <span id="ddk_gdi_color_space_conversions_gg"></span><span id="DDK_GDI_COLOR_SPACE_CONVERSIONS_GG"></span>


GDI 使用三个 RGB 颜色空间作为位图表示形式。 在其中的每个颜色空间中，三个位域或 *颜色通道* 用于分别指定红色、绿色和蓝色的位数。 为了能够使 GDI 的功能与位图匹配，视频驱动程序必须能够从一个 RGB 颜色空间转换到另一个 RGB 颜色空间。

GDI 可识别以下 RGB 颜色空间：

-   5:5:5 RGB：红色、绿色和蓝色的五位颜色通道

-   5:6:5 RGB：红色的五位颜色通道、绿色的六位颜色通道和蓝色的五位颜色通道

-   8:8:8 RGB：红色、绿色和蓝色的8位颜色通道

通常，从具有更多位数的颜色通道转换为一个具有较少位的颜色通道时，GDI 会丢弃低序位。 当转换从具有较少位数的颜色通道转换为一个具有更多位数的颜色通道时，较小通道的所有位都将复制到较大的通道。 若要填写更大通道的其余部分，请将较小通道的一些位数再次复制到较大的通道。 下表总结了 GDI 用于从一个 RGB 颜色空间转换到另一个颜色空间的规则。 在此表中，转换中值更改的颜色通道显示为 **粗体** 。

### <a name="span-idgdi_color_space_conversion_rulesspanspan-idgdi_color_space_conversion_rulesspanspan-idgdi_color_space_conversion_rulesspangdi-color-space-conversion-rules"></a><span id="GDI_Color_Space_Conversion_Rules"></span><span id="gdi_color_space_conversion_rules"></span><span id="GDI_COLOR_SPACE_CONVERSION_RULES"></span>GDI 颜色空间转换规则

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">From</th>
<th align="left">功能</th>
<th align="left">规则</th>
<th align="left">示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>源的绿色通道 (MSB) 的最高有效位将追加到目标绿色通道的低序位端。</p></td>
<td align="left"><p> (0x15， <strong>0x19</strong>，0x1D) 成为</p>
<div>
 
</div>
 (0x15、 <strong>0x33</strong>、0x1D) 
<div>
 
</div>
请注意，仅绿色通道发生变化。 源的5位通道值为 1 1001，以二进制形式转换为6位值 11 0011。</td>
</tr>
<tr class="even">
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>对于每个通道，会将源通道的三个 MSBs 附加到目标通道的下端。</p></td>
<td align="left"><p> (<strong>0x15</strong>， <strong>0x19</strong>， <strong>0x1D</strong>) 成为</p>
<div>
 
</div>
 (<strong>0xAD</strong>、 <strong>0xCE</strong>、 <strong>0xEF</strong>) 
<div>
 
</div>
在红色通道中，1 0101 变成 1010 1101。 绿色和蓝色通道中发生类似的更改。</td>
</tr>
<tr class="odd">
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>丢弃源绿色频道 (LSB) 的最小有效位。</p></td>
<td align="left"><p> (0x15， <strong>0x33</strong>，0x1D) 成为</p>
<div>
 
</div>
 (0x15、 <strong>0x19</strong>、0x1D) 
<div>
 
</div>
请注意，仅绿色通道发生变化。 丢弃最低位
<div>
 
</div>
为 11 0011 以获取 1 1001。</td>
</tr>
<tr class="even">
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>对于源的5位 (红色和蓝色) 通道，从源复制三个 MSBs，并将其附加到目标的更低顺序端。 对于6位绿色通道，复制源中的两个 MSBs，并将其附加到目标的更低顺序端。</p></td>
<td align="left"><p> (<strong>0x15</strong>， <strong>0x33</strong>， <strong>0x1D</strong>) 成为</p>
<div>
 
</div>
 (<strong>0xAD</strong>、 <strong>0xCF</strong>、 <strong>0xEF</strong>) 
<div>
 
</div>
在红色通道中，1 0101 变成 1010 1101。 在绿色通道中，11 myhpccn-0011 变为
<div>
 
</div>
1100 1111。 蓝色通道中的转换类似于红色通道的变换。</td>
</tr>
<tr class="odd">
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>丢弃来自源的每个通道的三个 LSBs。</p></td>
<td align="left"><p> (<strong>0xAB</strong>， <strong>0xCD</strong>， <strong>0xEF</strong>) 成为</p>
<div>
 
</div>
 (<strong>0x15</strong>、 <strong>0x19</strong>、 <strong>0x1D</strong>) 
<div>
 
</div>
在红色通道中，1010 1011 变成 1 0101。 类似的转换发生在另两个通道中。</td>
</tr>
<tr class="even">
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>丢弃红和蓝通道中的三个 LSBs。 丢弃绿色通道中的两个 LSBs。</p></td>
<td align="left"><p> (<strong>0xAB</strong>， <strong>0xCD</strong>， <strong>0xEF</strong>) 成为</p>
<div>
 
</div>
 (<strong>0x15</strong>、 <strong>0x33</strong>、 <strong>0x1D</strong>) 
<div>
 
</div>
在绿色通道中，1100 1101 变成 11 0011。 红和蓝通道中的更改与以前列出的转换的更改相同。</td>
</tr>
</tbody>
</table>

 

 

 





