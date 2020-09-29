---
title: GDI 浮点服务
description: GDI 浮点服务
ms.assetid: 7e32c683-ffad-4a95-9c3a-6716f7ce20cb
keywords:
- GDI WDK Windows 2000 显示，浮点操作
- 图形驱动程序 WDK Windows 2000 显示，浮点操作
- 绘制 WDK GDI，浮点操作
- 浮点运算 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f10c806d97ef943264a061d7de8ea60172c3af
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423628"
---
# <a name="gdi-floating-point-services"></a>GDI 浮点服务


## <span id="ddk_gdi_floating_point_services_gg"></span><span id="DDK_GDI_FLOATING_POINT_SERVICES_GG"></span>


内核模式图形驱动程序必须在调用 GDI 提供的 [**EngSaveFloatingPointState**](/windows/win32/api/winddi/nf-winddi-engsavefloatingpointstate) 和 [**EngRestoreFloatingPointState**](/windows/win32/api/winddi/nf-winddi-engrestorefloatingpointstate) 例程之间执行所有浮点运算。

如果硬件具有浮点处理器，则驱动程序可以直接执行浮点运算。 否则，驱动程序可以使用下表中所示的 GDI [**FLOATOBJ**](/windows/win32/api/winddi/ns-winddi-floatobj) 服务来模拟浮点运算。 无论采用哪种处理器类型，驱动程序在声明浮点值时都应使用 FLOATL 数据类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engrestorefloatingpointstate" data-raw-source="[&lt;strong&gt;EngRestoreFloatingPointState&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engrestorefloatingpointstate)"><strong>EngRestoreFloatingPointState</strong></a></p></td>
<td align="left"><p>驱动程序使用任何浮点或 MMX 硬件指令后，还原 Windows 2000 和更高版本的内核浮点状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engsavefloatingpointstate" data-raw-source="[&lt;strong&gt;EngSaveFloatingPointState&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engsavefloatingpointstate)"><strong>EngSaveFloatingPointState</strong></a></p></td>
<td align="left"><p>保存当前的 Windows 2000 和更高版本的内核浮点状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_add" data-raw-source="[&lt;strong&gt;FLOATOBJ_Add&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_add)"><strong>FLOATOBJ_Add</strong></a></p></td>
<td align="left"><p>添加两个 FLOATOBJs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_addfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddFloat&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_addfloat)"><strong>FLOATOBJ_AddFloat</strong></a></p></td>
<td align="left"><p>添加一个 FLOATOBJ 和一个 FLOATL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_addlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_addlong)"><strong>FLOATOBJ_AddLong</strong></a></p></td>
<td align="left"><p>添加 FLOATOBJ 和 LONG。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_div" data-raw-source="[&lt;strong&gt;FLOATOBJ_Div&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_div)"><strong>FLOATOBJ_Div</strong></a></p></td>
<td align="left"><p>将一个 FLOATOBJ 除以另一个。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_divfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivFloat&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_divfloat)"><strong>FLOATOBJ_DivFloat</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 除以 FLOATL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_divlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_divlong)"><strong>FLOATOBJ_DivLong</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 除以 LONG。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_equal" data-raw-source="[&lt;strong&gt;FLOATOBJ_Equal&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_equal)"><strong>FLOATOBJ_Equal</strong></a></p></td>
<td align="left"><p>确定两个 FLOATOBJs 是否相等。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_equallong" data-raw-source="[&lt;strong&gt;FLOATOBJ_EqualLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_equallong)"><strong>FLOATOBJ_EqualLong</strong></a></p></td>
<td align="left"><p>确定 FLOATOBJ 和 LONG 是否相等。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_getfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetFloat&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_getfloat)"><strong>FLOATOBJ_GetFloat</strong></a></p></td>
<td align="left"><p>计算并返回 FLOATOBJ 的 FLOAT 等效值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_getlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_getlong)"><strong>FLOATOBJ_GetLong</strong></a></p></td>
<td align="left"><p>计算并返回 FLOATOBJ 的长等效值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_greaterthan" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThan&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_greaterthan)"><strong>FLOATOBJ_GreaterThan</strong></a></p></td>
<td align="left"><p>确定一个 FLOATOBJ 是否大于另一个。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_greaterthanlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThanLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_greaterthanlong)"><strong>FLOATOBJ_GreaterThanLong</strong></a></p></td>
<td align="left"><p>确定 FLOATOBJ 是否大于 LONG。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_lessthan" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThan&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_lessthan)"><strong>FLOATOBJ_LessThan</strong></a></p></td>
<td align="left"><p>确定一个 FLOATOBJ 是否小于另一个。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_lessthanlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThanLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_lessthanlong)"><strong>FLOATOBJ_LessThanLong</strong></a></p></td>
<td align="left"><p>确定 FLOATOBJ 是否小于 LONG。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_mul" data-raw-source="[&lt;strong&gt;FLOATOBJ_Mul&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_mul)"><strong>FLOATOBJ_Mul</strong></a></p></td>
<td align="left"><p>将两个 FLOATOBJ 值相乘。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_mulfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulFloat&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_mulfloat)"><strong>FLOATOBJ_MulFloat</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 与 FLOATL 相乘。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_mullong" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_mullong)"><strong>FLOATOBJ_MulLong</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 乘以 LONG。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_neg" data-raw-source="[&lt;strong&gt;FLOATOBJ_Neg&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_neg)"><strong>FLOATOBJ_Neg</strong></a></p></td>
<td align="left"><p>更改 FLOATOBJ 的符号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_setfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetFloat&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_setfloat)"><strong>FLOATOBJ_SetFloat</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 设置为特定 FLOATL 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_setlong" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_setlong)"><strong>FLOATOBJ_SetLong</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 设置为特定的 LONG 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_sub" data-raw-source="[&lt;strong&gt;FLOATOBJ_Sub&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_sub)"><strong>FLOATOBJ_Sub</strong></a></p></td>
<td align="left"><p>从一个 FLOATOBJ 中减去另一个。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_subfloat" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubFloat&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_subfloat)"><strong>FLOATOBJ_SubFloat</strong></a></p></td>
<td align="left"><p>从 FLOATOBJ 中减去 FLOATL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-floatobj_sublong" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubLong&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-floatobj_sublong)"><strong>FLOATOBJ_SubLong</strong></a></p></td>
<td align="left"><p>从 FLOATOBJ 中减去 LONG。</p></td>
</tr>
</tbody>
</table>

 

