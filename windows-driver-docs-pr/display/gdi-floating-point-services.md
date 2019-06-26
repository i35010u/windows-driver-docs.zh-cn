---
title: GDI 浮点服务
description: GDI 浮点服务
ms.assetid: 7e32c683-ffad-4a95-9c3a-6716f7ce20cb
keywords:
- GDI WDK Windows 2000 显示，浮点运算
- 图形驱动程序 WDK Windows 2000 显示，浮点运算
- 绘制 WDK GDI，浮点运算
- 浮点运算 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d822436b58aa3e1214fecc904c2197978c782e60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385674"
---
# <a name="gdi-floating-point-services"></a>GDI 浮点服务


## <span id="ddk_gdi_floating_point_services_gg"></span><span id="DDK_GDI_FLOATING_POINT_SERVICES_GG"></span>


内核模式图形驱动程序必须执行的 GDI 提供调用之间的所有浮点运算[ **EngSaveFloatingPointState** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)并[ **EngRestoreFloatingPointState** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)例程。

如果硬件浮点处理器，该驱动程序可以直接执行浮点运算。 否则，该驱动程序可以使用 GDI [ **FLOATOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_floatobj)显示下表来模拟浮点运算的服务。 而不考虑处理器类型，该驱动程序应使用 FLOATL 数据类型声明浮点值时。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate" data-raw-source="[&lt;strong&gt;EngRestoreFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)"><strong>EngRestoreFloatingPointState</strong></a></p></td>
<td align="left"><p>还原 Windows 2000 和更高版本内核浮点状态后的驱动程序使用任何浮点或 MMX 硬件指令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate" data-raw-source="[&lt;strong&gt;EngSaveFloatingPointState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate)"><strong>EngSaveFloatingPointState</strong></a></p></td>
<td align="left"><p>将保存当前的 Windows 2000 和更高版本内核浮点状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_add" data-raw-source="[&lt;strong&gt;FLOATOBJ_Add&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_add)"><strong>FLOATOBJ_Add</strong></a></p></td>
<td align="left"><p>将添加两个 FLOATOBJs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_addfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddFloat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_addfloat)"><strong>FLOATOBJ_AddFloat</strong></a></p></td>
<td align="left"><p>添加了 FLOATOBJ 和 FLOATL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_addlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_addlong)"><strong>FLOATOBJ_AddLong</strong></a></p></td>
<td align="left"><p>添加了 FLOATOBJ 和 long 类型的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_div" data-raw-source="[&lt;strong&gt;FLOATOBJ_Div&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_div)"><strong>FLOATOBJ_Div</strong></a></p></td>
<td align="left"><p>一个 FLOATOBJ 除以另一个。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_divfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivFloat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_divfloat)"><strong>FLOATOBJ_DivFloat</strong></a></p></td>
<td align="left"><p>除以 FLOATL FLOATOBJ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_divlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_divlong)"><strong>FLOATOBJ_DivLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ 除以 long 类型的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_equal" data-raw-source="[&lt;strong&gt;FLOATOBJ_Equal&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_equal)"><strong>FLOATOBJ_Equal</strong></a></p></td>
<td align="left"><p>确定两个 FLOATOBJs 是否相等。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_equallong" data-raw-source="[&lt;strong&gt;FLOATOBJ_EqualLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_equallong)"><strong>FLOATOBJ_EqualLong</strong></a></p></td>
<td align="left"><p>确定 FLOATOBJ 和 long 类型的值是否相等。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_getfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetFloat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_getfloat)"><strong>FLOATOBJ_GetFloat</strong></a></p></td>
<td align="left"><p>计算并返回 FLOATOBJ FLOAT 等效值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_getlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_getlong)"><strong>FLOATOBJ_GetLong</strong></a></p></td>
<td align="left"><p>计算并返回 FLOATOBJ 的 long 类型的值等效值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_greaterthan" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThan&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_greaterthan)"><strong>FLOATOBJ_GreaterThan</strong></a></p></td>
<td align="left"><p>确定是否大于另一个 FLOATOBJ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_greaterthanlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThanLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_greaterthanlong)"><strong>FLOATOBJ_GreaterThanLong</strong></a></p></td>
<td align="left"><p>确定是否 FLOATOBJ 大于 long 类型的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_lessthan" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThan&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_lessthan)"><strong>FLOATOBJ_LessThan</strong></a></p></td>
<td align="left"><p>确定一个 FLOATOBJ 是否小于另一个。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_lessthanlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThanLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_lessthanlong)"><strong>FLOATOBJ_LessThanLong</strong></a></p></td>
<td align="left"><p>确定是否 FLOATOBJ 小于较长。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_mul" data-raw-source="[&lt;strong&gt;FLOATOBJ_Mul&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_mul)"><strong>FLOATOBJ_Mul</strong></a></p></td>
<td align="left"><p>将两个 FLOATOBJ 值相乘。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_mulfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulFloat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_mulfloat)"><strong>FLOATOBJ_MulFloat</strong></a></p></td>
<td align="left"><p>返回由 FLOATL FLOATOBJ 的乘积。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_mullong" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_mullong)"><strong>FLOATOBJ_MulLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ 乘以 long 类型的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_neg" data-raw-source="[&lt;strong&gt;FLOATOBJ_Neg&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_neg)"><strong>FLOATOBJ_Neg</strong></a></p></td>
<td align="left"><p>更改 FLOATOBJ 的符号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_setfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetFloat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_setfloat)"><strong>FLOATOBJ_SetFloat</strong></a></p></td>
<td align="left"><p>设置为特定的 FLOATL 值 FLOATOBJ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_setlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_setlong)"><strong>FLOATOBJ_SetLong</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 设置为特定的长整型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_sub" data-raw-source="[&lt;strong&gt;FLOATOBJ_Sub&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_sub)"><strong>FLOATOBJ_Sub</strong></a></p></td>
<td align="left"><p>减去一个 FLOATOBJ 从另一个。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_subfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubFloat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_subfloat)"><strong>FLOATOBJ_SubFloat</strong></a></p></td>
<td align="left"><p>减去从 FLOATOBJ FLOATL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_sublong" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubLong&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-floatobj_sublong)"><strong>FLOATOBJ_SubLong</strong></a></p></td>
<td align="left"><p>减去从 FLOATOBJ long 类型的值。</p></td>
</tr>
</tbody>
</table>

 

 

 





