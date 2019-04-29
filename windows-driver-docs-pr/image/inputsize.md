---
title: InputSize 元素
description: 可选 InputSize 元素指定的原始扫描媒体的大小。
ms.assetid: 406cfff9-7357-467f-a07a-340e32d9220f
keywords:
- InputSize 元素成像设备
topic_type:
- apiref
api_name:
- wscn InputSize wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c983a30712fd93c9e31f275cc14e9a3b0af40b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326078"
---
# <a name="inputsize-element"></a>InputSize 元素


可选**InputSize**元素指定原始扫描媒体的大小。

<a name="usage"></a>用法
-----

```xml
<wscn:InputSize wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:InputSize wscn:MustHonor="">
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
<th>特性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子元素


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
<td><p><a href="documentsizeautodetect.md" data-raw-source="[&lt;strong&gt;DocumentSizeAutoDetect&lt;/strong&gt;](documentsizeautodetect.md)"><strong>DocumentSizeAutoDetect</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="inputmediasize.md" data-raw-source="[&lt;strong&gt;InputMediaSize&lt;/strong&gt;](inputmediasize.md)"><strong>InputMediaSize</strong></a></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**InputSize**元素可以包含[ **DocumentSizeAutoDetect** ](documentsizeautodetect.md)或者[ **InputMediaSize** ](inputmediasize.md)元素，但不可同时使用两者。 **DocumentSizeAutoDetect**指定设备自动检测到的原始页面大小。 **InputMediaSize**指定要进行扫描当前作业的媒体的大小。

客户端可以指定可选**MustHonor**属性时，才**InputSize**元素包含在**CreateScanJobRequest**层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅[ **CreateScanJobRequest**](createscanjobrequest.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**DocumentSizeAutoDetect**](documentsizeautodetect.md)

[**InputMediaSize**](inputmediasize.md)

 

 






