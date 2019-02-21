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
ms.openlocfilehash: 04f60fc29e5c710d31895016089e3b9a4887b736
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526567"
---
# <a name="gdi-floating-point-services"></a>GDI 浮点服务


## <span id="ddk_gdi_floating_point_services_gg"></span><span id="DDK_GDI_FLOATING_POINT_SERVICES_GG"></span>


内核模式图形驱动程序必须执行的 GDI 提供调用之间的所有浮点运算[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)并[ **EngRestoreFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565006)例程。

如果硬件浮点处理器，该驱动程序可以直接执行浮点运算。 否则，该驱动程序可以使用 GDI [ **FLOATOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565804)显示下表来模拟浮点运算的服务。 而不考虑处理器类型，该驱动程序应使用 FLOATL 数据类型声明浮点值时。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565006" data-raw-source="[&lt;strong&gt;EngRestoreFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565006)"><strong>EngRestoreFloatingPointState</strong></a></p></td>
<td align="left"><p>还原 Windows 2000 和更高版本内核浮点状态后的驱动程序使用任何浮点或 MMX 硬件指令。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565010" data-raw-source="[&lt;strong&gt;EngSaveFloatingPointState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565010)"><strong>EngSaveFloatingPointState</strong></a></p></td>
<td align="left"><p>将保存当前的 Windows 2000 和更高版本内核浮点状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565814" data-raw-source="[&lt;strong&gt;FLOATOBJ_Add&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565814)"><strong>FLOATOBJ_Add</strong></a></p></td>
<td align="left"><p>将添加两个 FLOATOBJs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565822" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565822)"><strong>FLOATOBJ_AddFloat</strong></a></p></td>
<td align="left"><p>添加了 FLOATOBJ 和 FLOATL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565826" data-raw-source="[&lt;strong&gt;FLOATOBJ_AddLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565826)"><strong>FLOATOBJ_AddLong</strong></a></p></td>
<td align="left"><p>添加了 FLOATOBJ 和 long 类型的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565835" data-raw-source="[&lt;strong&gt;FLOATOBJ_Div&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565835)"><strong>FLOATOBJ_Div</strong></a></p></td>
<td align="left"><p>一个 FLOATOBJ 除以另一个。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565841" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565841)"><strong>FLOATOBJ_DivFloat</strong></a></p></td>
<td align="left"><p>除以 FLOATL FLOATOBJ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565845" data-raw-source="[&lt;strong&gt;FLOATOBJ_DivLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565845)"><strong>FLOATOBJ_DivLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ 除以 long 类型的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565861" data-raw-source="[&lt;strong&gt;FLOATOBJ_Equal&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565861)"><strong>FLOATOBJ_Equal</strong></a></p></td>
<td align="left"><p>确定两个 FLOATOBJs 是否相等。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565870" data-raw-source="[&lt;strong&gt;FLOATOBJ_EqualLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565870)"><strong>FLOATOBJ_EqualLong</strong></a></p></td>
<td align="left"><p>确定 FLOATOBJ 和 long 类型的值是否相等。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565871" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565871)"><strong>FLOATOBJ_GetFloat</strong></a></p></td>
<td align="left"><p>计算并返回 FLOATOBJ FLOAT 等效值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565873" data-raw-source="[&lt;strong&gt;FLOATOBJ_GetLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565873)"><strong>FLOATOBJ_GetLong</strong></a></p></td>
<td align="left"><p>计算并返回 FLOATOBJ 的 long 类型的值等效值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565880" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThan&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565880)"><strong>FLOATOBJ_GreaterThan</strong></a></p></td>
<td align="left"><p>确定是否大于另一个 FLOATOBJ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565884" data-raw-source="[&lt;strong&gt;FLOATOBJ_GreaterThanLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565884)"><strong>FLOATOBJ_GreaterThanLong</strong></a></p></td>
<td align="left"><p>确定是否 FLOATOBJ 大于 long 类型的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565894" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThan&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565894)"><strong>FLOATOBJ_LessThan</strong></a></p></td>
<td align="left"><p>确定一个 FLOATOBJ 是否小于另一个。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565902" data-raw-source="[&lt;strong&gt;FLOATOBJ_LessThanLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565902)"><strong>FLOATOBJ_LessThanLong</strong></a></p></td>
<td align="left"><p>确定是否 FLOATOBJ 小于较长。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565908" data-raw-source="[&lt;strong&gt;FLOATOBJ_Mul&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565908)"><strong>FLOATOBJ_Mul</strong></a></p></td>
<td align="left"><p>将两个 FLOATOBJ 值相乘。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565914" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565914)"><strong>FLOATOBJ_MulFloat</strong></a></p></td>
<td align="left"><p>返回由 FLOATL FLOATOBJ 的乘积。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565916" data-raw-source="[&lt;strong&gt;FLOATOBJ_MulLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565916)"><strong>FLOATOBJ_MulLong</strong></a></p></td>
<td align="left"><p>FLOATOBJ 乘以 long 类型的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565919" data-raw-source="[&lt;strong&gt;FLOATOBJ_Neg&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565919)"><strong>FLOATOBJ_Neg</strong></a></p></td>
<td align="left"><p>更改 FLOATOBJ 的符号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565922" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565922)"><strong>FLOATOBJ_SetFloat</strong></a></p></td>
<td align="left"><p>设置为特定的 FLOATL 值 FLOATOBJ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565928" data-raw-source="[&lt;strong&gt;FLOATOBJ_SetLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565928)"><strong>FLOATOBJ_SetLong</strong></a></p></td>
<td align="left"><p>将 FLOATOBJ 设置为特定的长整型值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565935" data-raw-source="[&lt;strong&gt;FLOATOBJ_Sub&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565935)"><strong>FLOATOBJ_Sub</strong></a></p></td>
<td align="left"><p>减去一个 FLOATOBJ 从另一个。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565938" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubFloat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565938)"><strong>FLOATOBJ_SubFloat</strong></a></p></td>
<td align="left"><p>减去从 FLOATOBJ FLOATL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565941" data-raw-source="[&lt;strong&gt;FLOATOBJ_SubLong&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565941)"><strong>FLOATOBJ_SubLong</strong></a></p></td>
<td align="left"><p>减去从 FLOATOBJ long 类型的值。</p></td>
</tr>
</tbody>
</table>

 

 

 





