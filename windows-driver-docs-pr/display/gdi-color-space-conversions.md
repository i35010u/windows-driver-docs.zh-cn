---
title: GDI 色彩空间转换
description: GDI 色彩空间转换
ms.assetid: f1840d58-9f93-4aa3-8344-d5e61c176254
keywords:
- 图面协商 WDK GDI，颜色空间转换
- 颜色通道 WDK GDI
- 颜色空间转换 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21e5d5d99cc5e8cc0c0f11bfe51b46a0d916d20f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342396"
---
# <a name="gdi-color-space-conversions"></a>GDI 色彩空间转换


## <span id="ddk_gdi_color_space_conversions_gg"></span><span id="DDK_GDI_COLOR_SPACE_CONVERSIONS_GG"></span>


GDI 将三个 RGB 颜色空间用于其位图表示形式。 在每个这些颜色空间，三个位域，或*颜色通道*，用于指定红色、 绿色和蓝色，分别用于，在给定颜色的比特数。 为了能够匹配与位图的 GDI 的功能，必须能够从一个 RGB 颜色空间转换到另一个视频驱动程序。

GDI 识别以下的 RGB 颜色空间：

-   5:5:5 RGB： 红色、 绿色和蓝色的五位颜色通道

-   5:6:5 RGB： 红色、 绿色、 六位颜色通道和蓝色的五位颜色通道的五位颜色通道

-   8:8:8 RGB： 红色、 绿色和蓝色的 8 位颜色通道

一般情况下，当从具有更多位数的颜色通道转换为另一个使用较少的位，GDI 将放弃较低顺序位。 当从位数更少的颜色通道，转换将为具有更多位数时，较小的通道的位的所有复制到更大的通道。 填写剩余的位的较大的通道，一些较小的通道的位是再次复制到更大的通道。 下表总结了 GDI 用于从一个 RGB 颜色空间转换为另一规则。 在此表中，在转换过程中更改其值的颜色通道所示**粗体**字体样式。

### <a name="span-idgdicolorspaceconversionrulesspanspan-idgdicolorspaceconversionrulesspanspan-idgdicolorspaceconversionrulesspangdi-color-space-conversion-rules"></a><span id="GDI_Color_Space_Conversion_Rules"></span><span id="gdi_color_space_conversion_rules"></span><span id="GDI_COLOR_SPACE_CONVERSION_RULES"></span>GDI 颜色空间转换规则

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">从</th>
<th align="left">要</th>
<th align="left">规则</th>
<th align="left">示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>源的绿色通道的最高有效位 (MSB) 追加到目标的绿色通道低顺序结束。</p></td>
<td align="left"><p>(0x15， <strong>0x19</strong>、 0x1D) 将变为</p>
<div>
 
</div>
(0x15， <strong>0x33</strong>、 0x1D)
<div>
 
</div>
请注意，只有绿色通道更改。 源的 5 位通道值是 1 1001，转换为 6 位值，11 0011 的二进制文件中。</td>
</tr>
<tr class="even">
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>对于每个通道，源通道的三个 MSBs 追加到目标通道较低顺序结束。</p></td>
<td align="left"><p>(<strong>0x15</strong>， <strong>0x19</strong>， <strong>0x1D</strong>) 将变为</p>
<div>
 
</div>
(<strong>0xAD</strong>， <strong>0xCE</strong>， <strong>0xEF</strong>)
<div>
 
</div>
红色通道 1 0101年会成为 1010 1101年。 绿色和蓝色通道中发生类似更改。</td>
</tr>
<tr class="odd">
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>放弃源的绿色通道的最低有效的位 (LSB)。</p></td>
<td align="left"><p>(0x15， <strong>0x33</strong>、 0x1D) 将变为</p>
<div>
 
</div>
(0x15， <strong>0x19</strong>、 0x1D)
<div>
 
</div>
请注意，只有绿色通道更改。 放弃最低位
<div>
 
</div>
11 0011 获取 1 1001年。</td>
</tr>
<tr class="even">
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>源的 5 位 （红色和蓝色） 通道，将三个 MSBs 从源分片复制并将其追加到目标的较低序位末尾。 为 6 位绿色通道，将两个 MSBs 从源分片复制并将其追加到较低序位末尾的目标。</p></td>
<td align="left"><p>(<strong>0x15</strong>， <strong>0x33</strong>， <strong>0x1D</strong>) 将变为</p>
<div>
 
</div>
(<strong>0xAD</strong>， <strong>0xCF</strong>， <strong>0xEF</strong>)
<div>
 
</div>
红色通道 1 0101年会成为 1010 1101年。 在绿色通道 11 0011 变得
<div>
 
</div>
1100 1111. 蓝色通道中的转换是类似于红色通道。</td>
</tr>
<tr class="odd">
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>5:5:5</p></td>
<td align="left"><p>放弃的源的每个通道从三个 LSBs。</p></td>
<td align="left"><p>(<strong>0xAB</strong>， <strong>0xcd 填充</strong>， <strong>0xEF</strong>) 将变为</p>
<div>
 
</div>
(<strong>0x15</strong>， <strong>0x19</strong>， <strong>0x1D</strong>)
<div>
 
</div>
中的红色通道 1010 1011年变为 1 0101年。 类似的转换将在其他两个通道进行。</td>
</tr>
<tr class="even">
<td align="left"><p>8:8:8</p></td>
<td align="left"><p>5:6:5</p></td>
<td align="left"><p>放弃的红色和蓝色通道从三个 LSBs。 放弃两个 LSBs 从绿色通道。</p></td>
<td align="left"><p>(<strong>0xAB</strong>， <strong>0xcd 填充</strong>， <strong>0xEF</strong>) 将变为</p>
<div>
 
</div>
(<strong>0x15</strong>， <strong>0x33</strong>， <strong>0x1D</strong>)
<div>
 
</div>
在绿色通道 1100 1101年变得 11 0011。 红色和蓝色通道中的更改是转换的与上面列出相同。</td>
</tr>
</tbody>
</table>

 

 

 





