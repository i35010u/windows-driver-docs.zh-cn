---
title: 使用 GetOptionAttribute
description: 使用 GetOptionAttribute
ms.assetid: d35f0811-d572-422c-8672-ffd29bf69efa
keywords:
- GetOptionAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db41a468e2ba0a3aa2dc972ace848c4e1e304cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843614"
---
# <a name="using-getoptionattribute"></a>使用 GetOptionAttribute





只有 PPD 功能支持此函数。 如果某一属性不可用，则**GetOptionAttribute**将返回 E\_INVALIDARG。

在下表中， *pdwDataType*参数采用[**EATTRIBUTE\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype)枚举类型的值。

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
<p>pcbNeeded</em>： <em>pbData</em>指向的 Unicode 字符串的字节计数（包括 null 终止符）</p>
<p>此选项属性可用于<strong>EnumOptions</strong>可以在 PPD 功能上返回的任何选项。</p></td>
</tr>
<tr class="even">
<td><p><strong>调用</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_BINARY</p>
<p><em>pbData</em>：选项的 InvocationValue 的字节数组。</p>
<p>pcbNeeded</em>： <em>pbData</em>指向的二进制数据的字节计数</p>
<p>此选项属性可用于<strong>EnumOptions</strong>可以在 PPD 功能上返回的任何选项。 如果选项的 InvocationValue 为空，函数将按上述方式设置<em>pdwDataType</em> ，将 <em><em>pcbNeeded</em> = 0，然后返回 S_OK。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p></em>pdwDataType： kADT_LONG</p>
<p><em><em>pbData</em>：此选项的 PPD <em>OrderDependency 或 * NonUIOrderDependency 关键字指定的相对顺序。 请注意，这些关键字的第一个参数是一个实数，转换为 LONG，并返回。</p>
<p>pcbNeeded</em>： <strong>sizeof</strong>（LONG）</p>
<p>此选项特性仅适用于在 PPD 中具有 <em>OrderDependency 或 * NonUIOrderDependency 项的选项，并且该项不会省略 optionKeyword。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：以 null 结尾的 ASCII 字符串，其中包含以下部分名称之一： "ExitServer" "Prolog" "DocumentSetup" "PageSetup" "JCLSetup" "AnySetup"。</p>
<p>pcbNeeded</em>： <em>pbData</em>指向的 ASCII 字符串的字节计数（包括 null 终止符）</p>
<p>此选项特性仅适用于在 PPD 中具有 * OrderDependency 或 * NonUIOrderDependency 条目的选项，并且该条目不会省略 optionKeyword。</p></td>
</tr>
</tbody>
</table>

 

### <a name="output-parameters-for-specific-option-attributes"></a>特定选项属性的输出参数

除了前面所述的常规选项属性以外，下表中列出的选项属性在可用时可能会有限制。 某些属性可用于特定 PPD 功能的所有选项，而其他属性仅适用于其 PPD 功能的特定选项。 每个选项特性都列出了所有此类限制。

功能选项属性输出参数关键字 \*InputSlot

**RequiresPageRegion**

\*pdwDataType： kADT\_BOOL

*\*pbData*：如果必须随 \*InputSlot 调用代码一起发送 \*PageRegion 调用代码，**则为 TRUE** ; 否则为**FALSE** 。 这基于 PPD 的 \*RequiresPageRegion 关键字。 如果在此输入槽选项中省略关键字，则将为此属性返回**TRUE** 。

*\*pcbNeeded*： **sizeof**（BOOL）

除驱动程序生成的选项 "\*UseFormTrayTable" 外，此选项属性可用于 "InputSlot" PPD 功能的任何选项。

\*OutputBin

**OutputOrderReversed**

\*pdwDataType： kADT\_BOOL

*\*pbData*：如果 binOption 的输出顺序为 "反向"，则**为 TRUE** ; 如果输出顺序为 "Normal"，则为**FALSE** 。 这基于 PPD 的 \*DefaultOutputOrder 和 \*PageStackOrder 关键字。

*\*pcbNeeded*： **sizeof**（BOOL）

此选项属性可用于 "OutputBin" PPD 功能的任何选项。

\*PageSize

**ImageableArea**

\*pdwDataType： kADT\_RECT

*\*pbData*： PageSize 选项的可成像区域的边界框，如 PPD 的 \*ImageableArea 关键字指定的那样，将在 RECT 结构（在 Microsoft Windows SDK 文档中定义）中返回，其**左侧**和**下半**个成员包含 llx 和 lly 值，其**右**成员和**顶级**成员包含 urx 和 ury 值。 所有值都在 microns 中。 将 PPD 的 llx 和 lly 值向上舍入到最接近的整数，然后将其转换为 microns。 将 PPD 的 urx 和 ury 值向下舍入到最接近的整数，然后将其转换为 microns。

*\*pcbNeeded*： **sizeof**（RECT）

除 "CustomPageSize" 选项外，此选项属性可用于 "PageSize" PPD 功能的任何选项。

**PaperDimension**

\*pdwDataType： kADT\_大小

*\*pbData*：由 PPD 的 \*PaperDimension 关键字指定的 PageSize 选项的物理维度以大小结构（在 Windows SDK 文档中定义）返回，其**cx**成员包含宽度值，其**cy**成员包含高度值。 所有值都在 microns 中。

*\*pcbNeeded*： **sizeof**（SIZE）

除 "CustomPageSize" 选项外，此选项属性可用于 "PageSize" PPD 功能的任何选项。

\*PageSize： CustomPageSize

**HWMargins**

\*pdwDataType： kADT\_RECT

*\*pbData*：由 PPD 的 \*HWMargins 关键字指定的四个值在矩形结构中返回（在 Windows SDK 文档中定义）。 所有值都在 microns 中。

*\*pcbNeeded*： **sizeof**（RECT）

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

**MaxMediaHeight**

*\*pdwDataType*： KADT\_DWORD

*\*pbData*：由 PPD 的 \*MaxMediaHeight 关键字指定的值（在 microns 中）。

*\*pcbNeeded*： **sizeof**（DWORD）

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

**MaxMediaWidth**

*\*pdwDataType*： KADT\_DWORD

*\*pbData*：由 PPD 的 \*MaxMediaWidth 关键字指定的值（在 microns 中）。

*\*pcbNeeded*： **sizeof**（DWORD）

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

**ParamCustomPageSize**

*\*pdwDataType*： KADT\_CUSTOMSIZEPARAMS

*pbData*： CUSTOMPARAM\_最大元素数组，其中每个元素都是一个[**CUSTOMSIZEPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_customsizeparam)结构。 此数组的每个元素都存储在 PPD \*ParamCustomPageSize 关键字的 paramOption 条目中指定的值。 对于 "方向" 之外的 paramOption，lMinVal 和 lMaxVal 值都在 microns 中。 对于 "方向"，lMinVal 和 lMaxVal 值的范围是 \[0，3\]。

*\*pcbNeeded*： **sizeof**（CUSTOMSIZEPARAM） \* CUSTOMPARAM\_MAX

此选项特性仅适用于 "PageSize" PPD 功能的 "CustomPageSize" 选项。

请参阅以下说明。

\*InstalledMemory

**VMOption**

*\*pdwDataType*： KADT\_DWORD

*\*pbData*：由 ppd 的 \*VMOption 关键字指定的值; 如果 ppd 未指定此选项的 \*VMOption 关键字，则为0。

*\*pcbNeeded*： **sizeof**（DWORD）

此选项属性可用于 "InstalledMemory" PPD 功能的任何选项。

**FCacheSize**

*\*pdwDataType*： KADT\_DWORD

*\*pbData*：由 ppd 的 \*FCacheSize 关键字指定的值; 如果 ppd 未指定此选项的 \*FCacheSize 关键字，则为0。

*\*pcbNeeded*： **sizeof**（DWORD）

此选项属性可用于 "InstalledMemory" PPD 功能的任何选项。

 

### <a name="note-on-paramcustompagesize"></a>ParamCustomPageSize 上的注意事项

下面的示例代码演示如何获取 PPD 文件的 "\*ParamCustomPageSize Width" 条目的原始顺序、最小值和最大值。 在 printoem 中定义的 CUSTOMPARAM\_WIDTH 常量指示包含与 Width 项相关的信息的[**CUSTOMSIZEPARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_customsizeparam)结构的偏移量。 此结构是一种\_CUSTOMPARAM 的最大 CUSTOMSIZEPARAM 结构，构成此类结构的数组。 Printoem 标头定义一组名为 CUSTOMPARAM\_XXX，其中列出了此数组中结构的偏移量（Width、Height、WidthOffset、HeightOffset 和方向）。

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

 

 




