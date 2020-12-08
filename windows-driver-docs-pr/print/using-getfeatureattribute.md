---
title: 使用 GetFeatureAttribute
description: 使用 GetFeatureAttribute
keywords:
- GetFeatureAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 389800cb8471e77f70d1549a584fa7341d7fef26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785991"
---
# <a name="using-getfeatureattribute"></a>使用 GetFeatureAttribute





只有 PPD 功能支持此函数。 如果某一属性不可用，则 **GetFeatureAttribute** 将返回 E \_ INVALIDARG。

在下表中， *pdwDataType* 参数采用 [**EATTRIBUTE \_ DATATYPE**](/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype) 枚举类型的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能属性</th>
<th>输出参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DisplayName</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_UNICODE</p>
<p><em>pbData</em>：功能关键字名称的翻译字符串的以 null 结尾的 Unicode 字符串</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 Unicode 字符串的字节计数 (包含 null 终止符) </p>
<p>此功能属性可供任何 PPD 功能 <strong>EnumFeatures</strong> 返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefaultOption</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：默认选项关键字名称的以 null 结尾的 ASCII 字符串</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包含 null 终止符) </p>
<p>此功能属性可供任何 PPD 功能 <strong>EnumFeatures</strong> 返回。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OpenUIType</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：以 null 结尾的 ASCII 字符串，其中包含以下类型之一： "PickOne"、"PickMany"、"Boolean"。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包含 null 终止符) </p>
<p>此功能属性可供任何 PPD 功能 <strong>EnumFeatures</strong> 返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenGroupType</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：适用于在 PPD 的 " </em> OpenGroup： InstallableOptions ... <em>CloseGroup： InstallableOptions "对，将返回以 null 结尾的 ASCII 字符串" InstallableOptions "。 对于其他功能，将返回仅包含 null 终止符)  (的空 ASCII 字符串。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包含 null 终止符) </p>
<p>此功能属性可供 <strong>EnumFeatures</strong> 可以返回的任何 PPD 功能使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p><em>pdwDataType： kADT_LONG</p>
<p><em></em>pbData </em> ：此功能的 PPD 的 <em> OrderDependency 或 NonUIOrderDependency 关键字指定的相对顺序 <em> 。 请注意，这些关键字的第一个参数是一个实数，转换为 LONG，并返回。</p>
<p><em></em>pcbNeeded </em> ： <strong>SIZEOF</strong> (LONG) </p>
<p>此属性仅适用于 <em> 在 ppd 中具有 OrderDependency 或 * NonUIOrderDependency 条目的 ppd 功能，并且条目省略 optionKeyword。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p><em></em>pdwDataType </em> ： kADT_ASCII</p>
<p><em>pbData</em>：以 null 结尾的 ASCII 字符串，其中包含以下部分名称之一： "ExitServer"、"序言"、"DocumentSetup"、"PageSetup"、"JCLSetup" 或 "AnySetup"。</p>
<p><em></em>pcbNeeded </em> ： <em>pbData</em> 所指向的 ASCII 字符串的字节计数 (包含 null 终止符) </p>
<p>此属性仅适用于在 PPD 中具有 * OrderDependency 或 * NonUIOrderDependency 条目的 PPD 功能，并且条目省略 optionKeyword。</p></td>
</tr>
</tbody>
</table>

 

 

