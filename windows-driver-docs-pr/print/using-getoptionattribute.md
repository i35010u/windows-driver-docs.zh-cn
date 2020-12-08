---
title: 使用 GetOptionAttribute
description: 使用 GetOptionAttribute
keywords:
- GetOptionAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e587a58dea818a21b61847a31978673404a5e2ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785983"
---
# <a name="using-getoptionattribute"></a>使用 GetOptionAttribute





只有 PPD 功能支持此函数。 如果某一属性不可用，则 **GetOptionAttribute** 将返回 E \_ INVALIDARG。

在下表中， *pdwDataType* 参数采用 [**EATTRIBUTE \_ DATATYPE**](/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype) 枚举类型的值。

### <a name="output-parameters-for-general-option-attributes"></a>常规选项属性的输出参数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>常规选项属性</th>
<th>输出参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DisplayName</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_UNICODE</p>
<p><em>pbData</em>：以 null 结尾的选项关键字名称的翻译字符串的 Unicode 字符串</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 Unicode 字符串的字节计数 (包含 null 终止符) </p>
<p>此选项属性可用于 <strong>EnumOptions</strong> 可以在 PPD 功能上返回的任何选项。</p></td>
</tr>
<tr class="even">
<td><p><strong>调用</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_BINARY</p>
<p><em>pbData</em>：选项的 InvocationValue 的字节数组。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em>指向的二进制数据的字节计数</p>
<p>此选项属性可用于 <strong>EnumOptions</strong> 可以在 PPD 功能上返回的任何选项。 如果选项的 InvocationValue 为空，函数将按上述方式设置<em>pdwDataType</em> ，将 <em> <em>pcbNeeded</em>设置为0，然后返回 S_OK。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p></em>pdwDataType： kADT_LONG</p>
<p><em><em>pbData</em>：由 PPD 的 <em> OrderDependency 或 * NonUIOrderDependency 关键字为此选项指定的相对顺序。 请注意，这些关键字的第一个参数是一个实数，转换为 LONG，并返回。</p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (LONG) </p>
<p>此选项特性仅适用于 <em> 在 PPD 中具有 OrderDependency 或 * NonUIOrderDependency 项的选项，该项不会省略 optionKeyword。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_ASCII</p>
<p><em>pbData</em>：以 null 结尾的 ASCII 字符串，其中包含以下部分名称之一： "ExitServer" "Prolog" "DocumentSetup" "PageSetup" "JCLSetup" "AnySetup"。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包含 null 终止符) </p>
<p>此选项特性仅适用于在 PPD 中具有 * OrderDependency 或 * NonUIOrderDependency 条目的选项，并且该条目不会省略 optionKeyword。</p></td>
</tr>
</tbody>
</table>

 

### <a name="output-parameters-for-specific-option-attributes"></a>特定选项属性的输出参数

除了前面所述的常规选项属性以外，下表中列出的选项属性在可用时可能会有限制。 某些属性可用于特定 PPD 功能的所有选项，而其他属性仅适用于其 PPD 功能的特定选项。 每个选项特性都列出了所有此类限制。

功能选项特性 Output Parameters 关键字 \* InputSlot

**RequiresPageRegion**

\*pdwDataType： kADT \_ BOOL

*\* pbData*： **TRUE** \*PageRegion 调用代码必须与 \* InputSlot 调用代码一起发送，否则 **为 FALSE** 。 这基于 PPD 的 \* RequiresPageRegion 关键字。 如果在此输入槽选项中省略关键字，则将为此属性返回 **TRUE** 。

*\* pcbNeeded*： **sizeof** (BOOL) 

除驱动程序生成的选项 "UseFormTrayTable" 外，此选项属性可用于 "InputSlot" PPD 功能的任何选项 \* 。

\*OutputBin

**OutputOrderReversed**

\*pdwDataType： kADT \_ BOOL

*\* pbData*：如果 binOption 的输出顺序为 "反向"，则 **为 TRUE** ; 如果输出顺序为 "Normal"，则为 **FALSE** 。 这基于 PPD 的 \* DefaultOutputOrder 和 \* PageStackOrder 关键字。

*\* pcbNeeded*： **sizeof** (BOOL) 

此选项属性可用于 "OutputBin" PPD 功能的任何选项。

\*PageSize

**ImageableArea**

\*pdwDataType： kADT \_ RECT

*\* PbData*： PageSize 选项的成像区域的边界框，由 PPD 的 \*ImageableArea 关键字 (在 Microsoft Windows SDK 文档) 中定义的 RECT 结构中返回，其 **左侧** 和 **底部** 成员包含 llx 和 lly 值，其 **右侧** 和 **顶部** 成员包含 urx 和 ury 值。 所有值都在 microns 中。 将 PPD 的 llx 和 lly 值向上舍入到最接近的整数，然后将其转换为 microns。 将 PPD 的 urx 和 ury 值向下舍入到最接近的整数，然后将其转换为 microns。

*\* pcbNeeded*： **sizeof** (RECT) 

除 "CustomPageSize" 选项外，此选项属性可用于 "PageSize" PPD 功能的任何选项。

**PaperDimension**

\*pdwDataType： kADT \_ SIZE

*\* PbData*： PageSize 选项的物理维度，由 PPD 的 \*PaperDimension 关键字在 Windows SDK 文档) 中定义 (大小结构中，其 **cx** 成员包含 width 值并且其 **cy** 成员包含高度值。 所有值都在 microns 中。

*\* pcbNeeded*： **sizeof** (大小) 

除 "CustomPageSize" 选项外，此选项属性可用于 "PageSize" PPD 功能的任何选项。

\*PageSize： CustomPageSize

**HWMargins**

\*pdwDataType： kADT \_ RECT

*\* pbData*：由 PPD 的 \* (在 Windows SDK 文档) 中定义的 RECT 结构中返回 HWMargins 关键字。 所有值都在 microns 中。

*\* pcbNeeded*： **sizeof** (RECT) 

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

**MaxMediaHeight**

*\* pdwDataType*： kADT \_DWORD

*\* pbData*：由 PPD 的 \*MaxMediaHeight 关键字，在 microns 中。

*\* pcbNeeded*： **sizeof** (DWORD) 

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

**MaxMediaWidth**

*\* pdwDataType*： kADT \_DWORD

*\* pbData*：由 PPD 的 \*MaxMediaWidth 关键字，在 microns 中。

*\* pcbNeeded*： **sizeof** (DWORD) 

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

**ParamCustomPageSize**

*\* pdwDataType*： kADT \_CUSTOMSIZEPARAMS

*pbData*： CUSTOMPARAM \_ MAX 元素的数组，其中每个元素都是一个 [**CUSTOMSIZEPARAM**](/windows-hardware/drivers/ddi/printoem/ns-printoem-_customsizeparam) 结构。 此数组的每个元素都存储在 PPD 的 \* ParamCustomPageSize 关键字的 paramOption 条目中指定的值。 对于 "方向" 之外的 paramOption，lMinVal 和 lMaxVal 值都在 microns 中。 对于 "方向"，lMinVal 和 lMaxVal 值的范围为 \[ 0，3 \] 。

*\* pcbNeeded*： **sizeof** (CUSTOMSIZEPARAM) \*\_最大 CUSTOMPARAM

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

请参阅以下说明。

\*InstalledMemory

**VMOption**

*\* pdwDataType*： kADT \_DWORD

*\* pbData*：由 PPD 的 \*VMOption 关键字，如果 PPD 未指定 \* 此选项的 VMOption 关键字，则为0。

*\* pcbNeeded*： **sizeof** (DWORD) 

此选项属性可用于 "InstalledMemory" PPD 功能的任何选项。

**FCacheSize**

*\* pdwDataType*： kADT \_DWORD

*\* pbData*：由 PPD 的 \*FCacheSize 关键字，如果 PPD 未指定 \* 此选项的 FCacheSize 关键字，则为0。

*\* pcbNeeded*： **sizeof** (DWORD) 

此选项属性可用于 "InstalledMemory" PPD 功能的任何选项。

 

### <a name="note-on-paramcustompagesize"></a>ParamCustomPageSize 上的注意事项

下面的示例代码演示如何获取 PPD 文件的 " \* ParamCustomPageSize Width" 条目的原始顺序、最小值和最大值。 \_在 printoem 中定义的 CUSTOMPARAM WIDTH 常量指示包含与 WIDTH 项相关的信息的 [**CUSTOMSIZEPARAM**](/windows-hardware/drivers/ddi/printoem/ns-printoem-_customsizeparam)结构的偏移量。 此结构是一种 CUSTOMPARAM 的 \_ 最大 CUSTOMSIZEPARAM 结构，构成此类结构的数组。 Printoem 标头定义了一组名为 CUSTOMPARAM XXX 的常量 \_ ，其中列出了此数组中结构的偏移量 (Width、Height、WidthOffset、HeightOffset 和取向) 。

```cpp
PCUSTOMSIZEPARAM  pCSParam;

pCSParam = (PCUSTOMSIZEPARAM)pbData + CUSTOMPARAM_WIDTH;

order = pCSParam->dwOrder;
// Convert lMinVal and lMaxVal from microns to points.
//   To convert microns to inches, divide by 25400.
//   To convert inches to points, multiply by 72.
min = pCSParam->lMinVal / 25400.0 * 72.0;
max = pCSParam->lMaxVal / 25400.0 * 72.0;
```

 

