---
title: 使用 GetOptionAttribute
description: 使用 GetOptionAttribute
ms.assetid: d35f0811-d572-422c-8672-ffd29bf69efa
keywords:
- GetOptionAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23f857b23a017d99b4640668d821dcb5bfd1c4f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379019"
---
# <a name="using-getoptionattribute"></a>使用 GetOptionAttribute





此函数仅支持 PPD 功能。 如果某个属性不可用， **GetOptionAttribute**返回 E\_INVALIDARG。

下表中*pdwDataType*参数接受值为[ **EATTRIBUTE\_数据类型**](https://msdn.microsoft.com/library/windows/hardware/ff548692)枚举类型。

### <a name="output-parameters-for-general-option-attributes"></a>输出参数的常规选项属性

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
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>pbData</em>： 选项关键字名称的翻译字符串的 null 终止的 Unicode 字符串</p>
<p>pcbNeeded</em>： 指向 Unicode 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此选项属性可供任何选项<strong>EnumOptions</strong> PPD 功能可以返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>调用</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_BINARY</p>
<p><em>pbData</em>： 选项的 InvocationValue 的字节数组。</p>
<p>pcbNeeded</em>： 指向二进制数据的字节数<em>pbData</em></p>
<p>此选项属性可供任何选项<strong>EnumOptions</strong> PPD 功能可以返回。 如果该选项的 InvocationValue 为空，函数将设置<em>pdwDataType</em>如上所示，设置<em> <em>pcbNeeded</em> = 0，，然后返回 S_OK。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p></em>pdwDataType: kADT_LONG</p>
<p><em><em>pbData</em>： 指定的 PPD 的相对顺序<em>OrderDependency 或 * NonUIOrderDependency 关键字，此选项。 请注意，这些关键字的第一个参数转换为 long 类型的值，并返回的实数。</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>（长整型）</p>
<p>此选项属性是仅适用于具有一个选项<em>OrderDependency 或 * 中 PPD NonUIOrderDependency 项和条目不能省略 optionKeyword。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: null 终止的 ASCII 字符串包含下列节名称之一："ExitServer""Prolog""DocumentSetup""PageSetup""JCLSetup""AnySetup"。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此选项属性是仅适用于具有一个选项 * OrderDependency 或 * 中 PPD NonUIOrderDependency 项和条目不能省略 optionKeyword。</p></td>
</tr>
</tbody>
</table>

 

### <a name="output-parameters-for-specific-option-attributes"></a>输出参数的特定选项属性

除了前面所述的常规选项属性下, 表中列出的选项属性可能会限制可用时。 某些属性可供所有选项的特定 PPD 功能，而有些则是仅供其 PPD 功能的特定选项。 为每个选项属性列出了任何此类限制。

功能选择属性输出参数关键字\*InputSlot

**RequiresPageRegion**

\*pdwDataType: kADT\_BOOL

*\*pbData*:**TRUE**如果\*PageRegion 调用代码必须与发送\*InputSlot 调用代码，并**FALSE**否则为。 这基于 PPD \*RequiresPageRegion 关键字。 如果此输入槽选项时，省略了关键字 **，则返回 TRUE**此属性的返回。

*\*pcbNeeded*: **sizeof**(BOOL)

此选项属性可供任何选项"InputSlot"PPD 功能，除了驱动程序生成选项"\*UseFormTrayTable"。

\*OutputBin

**OutputOrderReversed**

\*pdwDataType: kADT\_BOOL

*\*pbData*:**TRUE**如果 binOption 的输出顺序是"反向"，并**FALSE**如果输出顺序为"Normal"。 这基于 PPD \*DefaultOutputOrder 和\*PageStackOrder 关键字。

*\*pcbNeeded*: **sizeof**(BOOL)

此选项属性可供任何选项"OutputBin"PPD 功能。

\*PageSize

**ImageableArea**

\*pdwDataType: kADT\_RECT

*\*pbData*: PageSize 选项成像区域，由 PPD 的指定边界框\*ImageableArea 关键字中返回 （在 Microsoft Windows SDK 文档中定义） 的 RECT 结构，它的**留**并**底部**llx 和是否手动值和其包含的成员**右**并**顶部**成员包含 urx 和 ury 值。 所有值都均以微米。 PPD llx 手动值向上舍入到最接近的整数转换为微米之前。 PPD urx 和 ury 值是向下舍入到最接近的整数转换为微米之前。

*\*pcbNeeded*: **sizeof**(RECT)

此选项属性可供任何选项"PageSize"PPD 功能，除"CustomPageSize"选项。

**PaperDimension**

\*pdwDataType: kADT\_SIZE

*\*pbData*: PageSize 选项，PPD 的由指定的物理维度\*PaperDimension 关键字是结构中返回大小 （在 Windows SDK 文档中定义），其**cx**成员包含宽度值并且其**cy**成员包含的高度值。 所有值都均以微米。

*\*pcbNeeded*: **sizeof**（大小）

此选项属性可供任何选项"PageSize"PPD 功能，除"CustomPageSize"选项。

\*PageSize:CustomPageSize

**HWMargins**

\*pdwDataType: kADT\_RECT

*\*pbData*： 指定的 PPD 的四个值\*HWMargins 关键字返回 RECT 结构 （在 Windows SDK 文档中定义） 中。 所有值都均以微米。

*\*pcbNeeded*: **sizeof**(RECT)

此选项属性是仅供"PageSize"PPD"CustomPageSize"选择功能。

**MaxMediaHeight**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*： 指定的 PPD 的值\*MaxMediaHeight 关键字，微米中的。

*\*pcbNeeded*: **sizeof**(DWORD)

此选项属性是仅供"PageSize"PPD"CustomPageSize"选择功能。

**MaxMediaWidth**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*： 指定的 PPD 的值\*MaxMediaWidth 关键字，微米中的。

*\*pcbNeeded*: **sizeof**(DWORD)

此选项属性是仅供"PageSize"PPD"CustomPageSize"选择功能。

**ParamCustomPageSize**

*\*pdwDataType*: kADT\_CUSTOMSIZEPARAMS

*pbData*： 数组 CUSTOMPARAM\_最大元素，其中每个元素都[ **CUSTOMSIZEPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff547337)结构。 此数组的每个元素将存储的 PPD 中指定的值\*ParamCustomPageSize 关键字 paramOption 条目。 对于"方向"以外的 paramOption，lMinVal 和 lMaxVal 值为微米中。 对于"方向"lMinVal 和 lMaxVal 的值为范围内的\[0，3 个\]。

*\*pcbNeeded*: **sizeof**(CUSTOMSIZEPARAM) \* CUSTOMPARAM\_最大值

此选项属性是仅供"PageSize"PPD"CustomPageSize"选择功能。

请参阅以下说明。

\*InstalledMemory

**VMOption**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*： 指定的 PPD 的值\*VMOption 关键字，或者，如果未指定 PPD 0 \*VMOption 关键字，此选项。

*\*pcbNeeded*: **sizeof**(DWORD)

此选项属性可供任何选项"InstalledMemory"PPD 功能。

**FCacheSize**

*\*pdwDataType*: kADT\_DWORD

*\*pbData*： 指定的 PPD 的值\*FCacheSize 关键字，或者，如果未指定 PPD 0 \*FCacheSize 关键字，此选项。

*\*pcbNeeded*: **sizeof**(DWORD)

此选项属性可供任何选项"InstalledMemory"PPD 功能。

 

### <a name="note-on-paramcustompagesize"></a>关于 ParamCustomPageSize 说明

下面是演示如何获取 PPD 文件的原始顺序、 最小和最大值的一些示例代码"\*ParamCustomPageSize 宽度"条目。 CUSTOMPARAM\_printoem.h 中定义，宽度常量表示的偏移量[ **CUSTOMSIZEPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff547337)与宽度条目相关的结构，它包含的信息。 此结构是一个 CUSTOMPARAM\_形成此类结构的数组的最大 CUSTOMSIZEPARAM 结构。 Printoem.h 标头定义一组常量名为 CUSTOMPARAM\_XXX 列出此数组 （宽度、 高度、 WidthOffset、 HeightOffset 和方向） 中的结构的偏移量。

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

 

 




