---
title: 使用 GetFeatureAttribute
description: 使用 GetFeatureAttribute
ms.assetid: e5050cb1-c178-405d-bb0e-fd7827198bca
keywords:
- GetFeatureAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89cc57d697891557e9848a7f0c1cf83e0eb38950
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843618"
---
# <a name="using-getfeatureattribute"></a>使用 GetFeatureAttribute





只有 PPD 功能支持此函数。 如果某一属性不可用，则**GetFeatureAttribute**将返回 E\_INVALIDARG。

在下表中， *pdwDataType*参数采用[**EATTRIBUTE\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ne-printoem-_eattribute_datatype)枚举类型的值。

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
<p>pcbNeeded</em>： <em>pbData</em>指向的 Unicode 字符串的字节计数（包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 功能<strong>EnumFeatures</strong>返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefaultOption</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：默认选项关键字名称的以 null 结尾的 ASCII 字符串</p>
<p>pcbNeeded</em>： <em>pbData</em>指向的 ASCII 字符串的字节计数（包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 功能<strong>EnumFeatures</strong>返回。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OpenUIType</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：以 null 结尾的 ASCII 字符串，其中包含以下类型之一： "PickOne"、"PickMany"、"Boolean"。</p>
<p>pcbNeeded</em>： <em>pbData</em>指向的 ASCII 字符串的字节计数（包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 功能<strong>EnumFeatures</strong>返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenGroupType</strong></p></td>
<td><p><em><em>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：对于在 PPD 的 "</em>OpenGroup： InstallableOptions ... <em>CloseGroup： InstallableOptions" 对中定义的功能，将返回以 null 结尾的 ASCII 字符串 "InstallableOptions"。 对于其他功能，将返回一个仅包含 null 终止符的空 ASCII 字符串。</p>
<p>pcbNeeded</em>： <em>pbData</em>指向的 ASCII 字符串的字节计数（包括 null 终止符）</p>
<p>此功能属性可供<strong>EnumFeatures</strong>可以返回的任何 PPD 功能使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p><em>pdwDataType： kADT_LONG</p>
<p>pbData</em>：由 PPD 的 <em>OrderDependency 或 <em>NonUIOrderDependency 关键字指定的相对顺序。 请注意，这些关键字的第一个参数是一个实数，转换为 LONG，并返回。</p>
<p>pcbNeeded</em>： <strong>sizeof</strong>（LONG）</p>
<p>此属性仅适用于在 PPD 中具有 <em>OrderDependency 或 * NonUIOrderDependency 项的 PPD 功能，该项忽略 optionKeyword。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p>pdwDataType</em>： kADT_ASCII</p>
<p><em>pbData</em>：以 null 结尾的 ASCII 字符串，其中包含以下部分名称之一： "ExitServer"、"序言"、"DocumentSetup"、"PageSetup"、"JCLSetup" 或 "AnySetup"。</p>
<p>pcbNeeded</em>： <em>pbData</em>指向的 ASCII 字符串的字节计数（包括 null 终止符）</p>
<p>此属性仅适用于在 PPD 中具有 * OrderDependency 或 * NonUIOrderDependency 条目的 PPD 功能，并且条目省略 optionKeyword。</p></td>
</tr>
</tbody>
</table>

 

 

 




