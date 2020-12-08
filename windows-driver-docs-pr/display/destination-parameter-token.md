---
title: 目标参数标记
description: 目标参数标记
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ee268b4632e32bb923d8eaf4ea2ffe6ae347b9ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809547"
---
# <a name="destination-parameter-token"></a>目标参数标记


## <span id="ddk_destination_parameter_token_gg"></span><span id="DDK_DESTINATION_PARAMETER_TOKEN_GG"></span>


目标参数令牌描述目标寄存器的属性，并且由以下位组成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>带宽

<span id="_10_00_"></span>**\[ 10:00 \]** 位0到10表示寄存器号)  (偏移量。

<span id="_12_11_"></span>**\[ 12:11 \]** 位11和12是 \[ \] 用于指示 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)的第四个和第五个第三位。

<span id="_13_"></span>**\[ 13 \]** 对于顶点着色器 (与) 版本 3 \_ 0 和更高版本，第13位表示是否使用相对寻址模式。 如果设置为1，则应用 [相对寻址](shader-relative-addressing.md) 。

对于所有像素着色器 (PS) 版本和顶点着色器版本低于 3 \_ 0，将保留第13位并将其设置为0x0。

<span id="_15_14_"></span>**\[ 15:14 \]** 已保留。 此值设置为0x0。

<span id="_19_16_"></span>**\[ 19:16 \]** 写入掩码。 此掩码的位具有以下组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bit</th>
<th align="left">组件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>组件 0 (X; 红色) </p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>组件 1 (Y;绿色) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>组件 2 (Z;蓝) </p></td>
</tr>
<tr class="even">
<td align="left"><p>19</p></td>
<td align="left"><p>组件 3 (W;Alpha) </p></td>
</tr>
</tbody>
</table>

 

<span id="_23_20_"></span>**\[ 23:20 \]** 位20到23表示结果修饰符。 可以使用多个结果修饰符。 以下结果修饰符类型可以在此4位值中运算在一起：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">Result 修饰符类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p> (顶点着色器的饱和) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>部分精度 (像素着色器) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>质心 (像素着色器) </p></td>
</tr>
</tbody>
</table>

 

<span id="_27_24_"></span>**\[ 27:24 \]** 对于低于 2 0 的 PS 版本 \_ ，0到27位指定 (签名移位) 的结果移位刻度。
对于 PS 版本 2 \_ 0 和更高版本以及 VS，将保留这些位并将其设置为0x0。
<span id="_30_28_"></span>**\[ 30:28 \]** 位28到30是 \[ \] 用于指示 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)的前三位0、1、2。

<span id="_31_"></span>**\[ 31 \]** 位31为0x1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

位28、29、30、11和12构成一个指示寄存器类型的5位值。 有关寄存器类型的信息，请参阅 [着色器寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

