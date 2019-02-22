---
title: 使用 GetFeatureAttribute
description: 使用 GetFeatureAttribute
ms.assetid: e5050cb1-c178-405d-bb0e-fd7827198bca
keywords:
- GetFeatureAttribute
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f8b02e4f82a0fa0254c40b8b5a72d98bde86ae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546865"
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
<p><em>pbData</em>： 将 Unicode 字符串以 null 结尾的功能关键字名称&#39;s 转换字符串</p>
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
<p><em>pbData</em>: null 终止的 ASCII 字符串包含以下类型之一：&quot;PickOne&quot;， &quot;PickMany&quot;，&quot;布尔&quot;。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 功能<strong>EnumFeatures</strong>可以返回。</p></td>
</tr>
<tr class="even">
<td><p><strong>OpenGroupType</strong></p></td>
<td><p><em><em>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>:PPD 中定义的功能&#39;s &quot; </em>OpenGroup:InstallableOptions...<em>CloseGroup:InstallableOptions&quot;配对的以 null 结尾的 ASCII 字符串&quot;InstallableOptions&quot;将返回。 对于其他功能，将返回一个空的 ASCII 字符串 （它具有仅 null 终止符）。</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此功能属性可供任何 PPD 的功能<strong>EnumFeatures</strong>可以返回。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OrderDependencyValue</strong></p></td>
<td><p><em>pdwDataType: kADT_LONG</p>
<p>pbData</em>： 指定 PPD 的相对顺序&#39;s <em>OrderDependency 或<em>NonUIOrderDependency 关键字为此功能。 请注意，这些关键字的第一个参数转换为 long 类型的值，并返回的实数。</p>
<p>pcbNeeded</em>: <strong>sizeof</strong>（长整型）</p>
<p>此属性是仅适用于具有的 PPD 功能<em>OrderDependency 或 * 中 PPD NonUIOrderDependency 入口和入口省略 optionKeyword。</p></td>
</tr>
<tr class="even">
<td><p><strong>OrderDependencySection</strong></p></td>
<td><p>pdwDataType</em>: kADT_ASCII</p>
<p><em>pbData</em>: null 终止的 ASCII 字符串包含下列节名称之一：&quot;ExitServer&quot;， &quot;Prolog&quot;， &quot;DocumentSetup&quot;， &quot;PageSetup&quot;， &quot;JCLSetup&quot;，或&quot;AnySetup&quot;.</p>
<p>pcbNeeded</em>： 指向 ASCII 字符串的字节数<em>pbData</em> （包括 null 终止符）</p>
<p>此属性是仅适用于具有的 PPD 功能 * OrderDependency 或 * 中 PPD NonUIOrderDependency 入口和入口省略 optionKeyword。</p></td>
</tr>
</tbody>
</table>

 

 

 




