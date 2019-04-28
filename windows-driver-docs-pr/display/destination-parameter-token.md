---
title: 目标参数标记
description: 目标参数标记
ms.assetid: 1a9842c5-0ea9-47ee-a341-77e705ab5e25
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc28ec9d6278727879b16ea290a366eb08d4d34e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348881"
---
# <a name="destination-parameter-token"></a>目标参数标记


## <span id="ddk_destination_parameter_token_gg"></span><span id="DDK_DESTINATION_PARAMETER_TOKEN_GG"></span>


目标参数标记描述属性的目标寄存器并由组成以下位：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_10_00_"></span>**\[10:00\]** 位 0 到 10 指示寄存器号 （注册文件中的偏移量）。

<span id="_12_11_"></span>**\[12:11\]**  bits 11 和 12 是第四个和第五个 bits \[3，4\]用于指示[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

<span id="_13_"></span>**\[13\]** 顶点着色器 (VS) 版本 3\_0 和更高版本，位 13 指示是否使用了相对的寻址模式。 如果设置为 1，[相对寻址](shader-relative-addressing.md)适用。

对所有像素着色器 (PS) 版本和顶点着色器版本早于 3\_0，13 位是保留，设为 0x0。

<span id="_15_14_"></span>**\[15:14\]** 保留。 此值设置为 0x0。

<span id="_19_16_"></span>**\[19:16\]** 写掩码。 此掩码的位具有以下组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
<th align="left">组件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>组件 (0x;红色）</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>组件 1 (Y;绿色）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>组件 2 (Z;蓝色）</p></td>
</tr>
<tr class="even">
<td align="left"><p>19</p></td>
<td align="left"><p>组件 3 (W;Alpha)</p></td>
</tr>
</tbody>
</table>

 

<span id="_23_20_"></span>**\[23:20\]** 位 20 到 23 表示结果修饰符。 可以使用多个结果修饰符。 以下结果修饰符类型可以是或运算一起此 4 位的值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">结果修饰符类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>饱和 （顶点着色器）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>部分精度 （像素着色器）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>质心 （像素着色器）</p></td>
</tr>
</tbody>
</table>

 

<span id="_27_24_"></span>**\[27:24\]** 早于 2 的 PS 版本\_0，24 到 27 位指定结果 shift 刻度 (有符号 shift)。
PS 版本 2 的\_0 和更高版本和 VS，这些位均为保留并且已设置为 0x0。
<span id="_30_28_"></span>**\[30:28\]** 到 30 位 28 个为前三个位\[0,1,2\]用于指示[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

<span id="_31_"></span>**\[31\]** 位 31 为 0x1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

28、 29、 30、 11 和 12 位窗体为 5 位值，该值指示注册类型。 有关注册类型的信息，请参阅[着色器注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





