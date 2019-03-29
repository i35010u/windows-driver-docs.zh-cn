---
title: 使用 GetFeatureAttribute
description: 使用 GetFeatureAttribute
ms.assetid: e5050cb1-c178-405d-bb0e-fd7827198bca
keywords:
- GetFeatureAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 934b53fe996ec01faf25c370684262efb6ac0f07
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463971"
---
# <a name="using-getfeatureattribute"></a>使用 GetFeatureAttribute





此函数仅支持 PPD 功能。 如果某个属性不可用， **GetFeatureAttribute**返回 E\_INVALIDARG。

下表中*pdwDataType*参数接受值为[ **EATTRIBUTE\_数据类型**](https://msdn.microsoft.com/library/windows/hardware/ff548692)枚举类型。

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
<td><p><em><em>pdwDataType</em>: kADT_UNICODE</p>
<p><em>pbData</em>： 功能关键字名称的翻译字符串的 null 终止的 Unicode 字符串</p>
<p>pcbNeeded</em>： 指向 Unicode 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 功能<strong>EnumFeatures</strong>可以返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>DefaultOption</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: null 终止的 ASCII 字符串的默认选项关键字名称</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 功能<strong>EnumFeatures</strong>可以返回。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OpenUIType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: null 终止的 ASCII 字符串包含以下类型之一："PickOne"，"PickMany"，"Boolean"。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 功能<strong>EnumFeatures</strong>可以返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenGroupType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:PPD 中定义的功能"</em>OpenGroup:InstallableOptions...<em>CloseGroup:InstallableOptions"对，将返回"InstallableOptions"的以 null 结尾的 ASCII 字符串。 对于其他功能，将返回一个空的 ASCII 字符串 （它具有仅 null 终止符）。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 的功能<strong>EnumFeatures</strong>可以返回。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p><em>pdwDataType: kADT_LONG</p>
<p>pbData</em>： 指定的 PPD 的相对顺序<em>OrderDependency 或<em>NonUIOrderDependency 关键字为此功能。 请注意，这些关键字的第一个参数转换为 long 类型的值，并返回的实数。</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>（长整型）</p>
<p>此属性是仅适用于具有的 PPD 功能<em>OrderDependency 或 * 中 PPD NonUIOrderDependency 入口和入口省略 optionKeyword。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: null 终止的 ASCII 字符串包含下列节名称之一："ExitServer"、"Prolog"、"DocumentSetup"、"PageSetup"、"JCLSetup"或者"AnySetup"。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此属性是仅适用于具有的 PPD 功能 * OrderDependency 或 * 中 PPD NonUIOrderDependency 入口和入口省略 optionKeyword。</p></td>
</tr>
</tbody>
</table>

 

 

 




