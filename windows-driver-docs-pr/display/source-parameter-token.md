---
title: 源参数标记
description: 源参数标记
ms.assetid: 280b9fb2-9b5c-4830-9ba5-cfb6201960e0
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b68529bb18f761446865e58d85644f22b7d6b28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545380"
---
# <a name="source-parameter-token"></a>源参数标记


## <span id="ddk_source_parameter_token_gg"></span><span id="DDK_SOURCE_PARAMETER_TOKEN_GG"></span>


源参数令牌描述源注册的属性，它是组成以下位：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_10_00_"></span>**\[10:00\]** 位 0 到 10 指示寄存器号 （注册文件中的偏移量）。

<span id="_12_11_"></span>**\[12:11\]**  bits 11 和 12 是第四个和第五个 bits \[3，4\]用于指示[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

<span id="_13_"></span>**\[13\]** 像素着色器 (PS) 版本早于 3\_0，13 位是保留，设为 0x0。

像素着色器 (PS) 版本 3 的\_0 和更高版本和所有版本的顶点着色器 (VS)，13 位都指示是否使用了相对的寻址模式。 如果设置为 1，[相对寻址](shader-relative-addressing.md)适用。

<span id="_15_14_"></span>**\[15:14\]** 保留所有的 PS 和 VS 版本。 此值设置为 0x0。

<span id="_23_16_"></span>**\[23:16\]**  bits 16 到 23 表示通道*swizzle*。 在四个执行所有算术运算 （X、 Y、 Z、 W） 并行通道。 Swizzle 指定哪些源组件参与操作的通道。 有关 swizzle 详细信息，请参阅最新的 DirectX SDK 文档。 此字段的位指定 swizzle 下列通道：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
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
<td align="left"><p>通道 W swizzle</p></td>
</tr>
</tbody>
</table>

 

上一位的任何一组中的以下值指定要在操作通道中使用的源组件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">Component</th>
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
<td align="left"><p>使用组件 W。</p></td>
</tr>
</tbody>
</table>

 

例如，如果 19:18 位设置为 0x2，然后组件 Z 用作通道 Y 操作源。

<span id="_27_24_"></span>**\[27:24\]** 位 24 到 27 指示源修饰符。 此 4 位的值指示以下源修饰符类型：

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
<td align="left"><p>求反</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>偏差</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>偏置和求反</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>登录 (bx2)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>登录 (bx2) 和负号</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>补数</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>x2 (PS 1_4)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>x2 和求反 (PS 1_4)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>dz （除通过由 Z 分量的 PS 1_4）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xa</p></td>
<td align="left"><p>数据仓库 (通过除以 W 组件 âˆ PS 1_4)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xb</p></td>
<td align="left"><p>abs(x) 计算绝对值</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xc</p></td>
<td align="left"><p>-abs(x) 计算绝对值的数值和求反</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xd</p></td>
<td align="left"><p>不。 仅应用于断言而注册，这是布尔值。 因此，它是逻辑非。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xe-0xf</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<span id="_30_28_"></span>**\[30:28\]** 到 30 位 28 个为前三个位\[0,1,2\]用于指示[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

<span id="_31_"></span>**\[31\]** 位 31 为 0x1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

28、 29、 30、 11 和 12 位窗体为 5 位值，该值指示注册类型。 有关注册类型的信息，请参阅[着色器注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





