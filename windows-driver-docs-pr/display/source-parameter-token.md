---
title: 源参数标记
description: 源参数标记
ms.assetid: 280b9fb2-9b5c-4830-9ba5-cfb6201960e0
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: cf2a09117d0260994ed2b9182273567f3c8d4746
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064602"
---
# <a name="source-parameter-token"></a>源参数标记


## <span id="ddk_source_parameter_token_gg"></span><span id="DDK_SOURCE_PARAMETER_TOKEN_GG"></span>


源参数标记描述源寄存器的属性，并且由以下位组成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>带宽

<span id="_10_00_"></span>** \[ 10:00 \] **位0到10表示寄存器号)  (偏移量。

<span id="_12_11_"></span>** \[ 12:11 \] **位11和12是 \[ \] 用于指示[寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)的第四个和第五个第三位。

<span id="_13_"></span>** \[ 13 \] **对于像素着色器 (PS) 低于 3 0 的版本 \_ ，将保留第13位并将其设置为0x0。

对于像素着色器 (PS) 版本 3 \_ 0 及更高版本，以及所有版本的顶点着色器 (与) ，第13位表示是否使用相对寻址模式。 如果设置为1，则应用 [相对寻址](shader-relative-addressing.md) 。

<span id="_15_14_"></span>** \[ 15:14 \] **为所有版本的 PS 和 VS 保留了。 此值设置为0x0。

<span id="_23_16_"></span>** \[ 23:16 \] **位16至23指示通道*swizzle*。 所有算术运算都按四 (X、Y、Z 和 W) 并行通道执行。 Swizzle 指定哪个源组件参与操作通道。 有关 swizzle 的详细信息，请参阅最新的 DirectX SDK 文档。 此字段的位为以下通道指定 swizzle：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bits</th>
<th align="left">通道</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>17:16</p></td>
<td align="left"><p>通道 X swizzle</p></td>
</tr>
<tr class="even">
<td align="left"><p>19:18</p></td>
<td align="left"><p>通道 Y swizzle</p></td>
</tr>
<tr class="odd">
<td align="left"><p>21:20</p></td>
<td align="left"><p>通道 Z swizzle</p></td>
</tr>
<tr class="even">
<td align="left"><p>23:22</p></td>
<td align="left"><p>频道 W swizzle</p></td>
</tr>
</tbody>
</table>

 

任何前一组位中的以下值指定要在操作通道中使用的源组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">组件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>使用组件 X。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>使用组件 Y。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>使用组件 Z。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>使用的组件 W。</p></td>
</tr>
</tbody>
</table>

 

例如，如果将19:18 位设置为0x2，则使用组件 Z 作为通道 Y 操作的源。

<span id="_27_24_"></span>** \[ 27:24 \] **位24到27表示源修饰符。 此4位值指示以下源修饰符类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">源修饰符类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>Negate</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>偏差</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>偏量和反运算</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>签署 (bx2) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>Sign (bx2) 和否定</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>补充</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>x2 (PS 1_4) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>x2 和否定 (PS 1_4) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>dz (通过 Z 分量除以-PS 1_4) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xa</p></td>
<td align="left"><p>dw (按 W 分量除以ˆ PS 1_4) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0xb</p></td>
<td align="left"><p>abs (x) 计算绝对值</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xc</p></td>
<td align="left"><p>-abs (x) 计算绝对值和反运算</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xd</p></td>
<td align="left"><p>不仅. 仅适用于断言而寄存器，后者为 BOOL。 因此，逻辑非。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xe-0xf</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<span id="_30_28_"></span>** \[ 30:28 \] **位28到30是 \[ \] 用于指示[寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)的前三位0、1、2。

<span id="_31_"></span>** \[ 31 \] **位31为0x1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

位28、29、30、11和12构成一个指示寄存器类型的5位值。 有关寄存器类型的信息，请参阅 [着色器寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

