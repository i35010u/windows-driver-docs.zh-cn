---
title: Height 元素
description: Height 元素指定扫描设备对需要高度的扫描程序配置元素所支持的高度值。
keywords:
- 高度元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Height wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ae70cedec8c0b17f0aa6290b31217fcb682408
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824131"
---
# <a name="height-element"></a>Height 元素


**Height** 元素指定扫描设备对需要高度的扫描程序配置元素所支持的高度值。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Height wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Height wscn:Override="" wscn:UsedDefault="">
```

<a name="attributes"></a>特性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>忽略</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 布尔值0、false、1或 true。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

必需。 有关可能的值，请参阅特定父元素。

## <a name="child-elements"></a>子元素


没有任何子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="heights.md" data-raw-source="[&lt;strong&gt;Heights&lt;/strong&gt;](heights.md)"><strong>Heights</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="inputmediasize.md" data-raw-source="[&lt;strong&gt;InputMediaSize&lt;/strong&gt;](inputmediasize.md)"><strong>InputMediaSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenmaximumsize.md" data-raw-source="[&lt;strong&gt;PlatenMaximumSize&lt;/strong&gt;](platenmaximumsize.md)"><strong>PlatenMaximumSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="platenminimumsize.md" data-raw-source="[&lt;strong&gt;PlatenMinimumSize&lt;/strong&gt;](platenminimumsize.md)"><strong>PlatenMinimumSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenopticalresolution.md" data-raw-source="[&lt;strong&gt;PlatenOpticalResolution&lt;/strong&gt;](platenopticalresolution.md)"><strong>PlatenOpticalResolution</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**Height** 元素的值取决于其父元素。 若要详细了解 **高度** 是必需的还是可选的以及有关其可能值的详细信息，请参阅相应的父值。

[**DocumentFinalParameters**](documentfinalparameters.md)

仅当 **Height** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定 optional **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**Heights**](heights.md)

[**InputMediaSize**](inputmediasize.md)

[**PlatenMaximumSize**](platenmaximumsize.md)

[**PlatenMinimumSize**](platenminimumsize.md)

[**PlatenOpticalResolution**](platenopticalresolution.md)

[**宽度**](width.md)

 

 






