---
title: 目标参数标记
description: 目标参数标记
ms.assetid: 1a9842c5-0ea9-47ee-a341-77e705ab5e25
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: abd2b827c3c0c5433a40809c1d6d62b5d891a432
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839015"
---
# <a name="destination-parameter-token"></a>目标参数标记


## <span id="ddk_destination_parameter_token_gg"></span><span id="DDK_DESTINATION_PARAMETER_TOKEN_GG"></span>


目标参数令牌描述目标寄存器的属性，并且由以下位组成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>带宽

<span id="_10_00_"></span> **\[10:00\]** 位0到10表示寄存器号（注册文件中的偏移量）。

<span id="_12_11_"></span> **\[12:11\]** 第四个和第五个位为第四个和第五个 \[3，4\]，用于指示[寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)。

<span id="_13_"></span> **\[13\]** 对于顶点着色器（VS）版本 3\_0 和更高版本，第13位表示是否使用相对寻址模式。 如果设置为1，则应用[相对寻址](shader-relative-addressing.md)。

对于低于 3\_0 的所有像素着色器（PS）版本和顶点着色器版本，将保留第13位并将其设置为0x0。

<span id="_15_14_"></span> **\[15:14\]** 保护. 此值设置为0x0。

<span id="_19_16_"></span> **\[19:16\]** 写入掩码。 此掩码的位具有以下组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">小段</th>
<th align="left">Component</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>组件0（X;红色</p></td>
</tr>
<tr class="even">
<td align="left"><p>17</p></td>
<td align="left"><p>组件1（Y;钩</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>组件2（Z;蓝色</p></td>
</tr>
<tr class="even">
<td align="left"><p>19</p></td>
<td align="left"><p>组件3（W;全角字</p></td>
</tr>
</tbody>
</table>

 

<span id="_23_20_"></span> **\[23:20\]** 位20到23表示结果修饰符。 可以使用多个结果修饰符。 以下结果修饰符类型可以在此4位值中运算在一起：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">Result 修饰符类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>饱和（顶点着色器）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>部分精度（像素着色器）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>质心（像素着色器）</p></td>
</tr>
</tbody>
</table>

 

<span id="_27_24_"></span> **\[27:24\]** 对于低于 2\_0 的 PS 版本，从24到27位的
对于 PS 版本 2\_0 和更高版本以及 VS，将保留这些位并将其设置为0x0。
<span id="_30_28_"></span> **\[30:28\]** 位28到30是用于指示[寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)\[0，1，2\] 的第三位。

<span id="_31_"></span> **\[31\]** 位31为0x1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

位28、29、30、11和12构成一个指示寄存器类型的5位值。 有关寄存器类型的信息，请参阅[着色器寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





