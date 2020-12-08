---
title: InputSize 元素
description: 可选的 InputSize 元素指定原始扫描介质的大小。
keywords:
- InputSize 元素图像设备
topic_type:
- apiref
api_name:
- wscn InputSize wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20c22b0accc6fb0703dbf2aec9106011e6060898
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793655"
---
# <a name="inputsize-element"></a>InputSize 元素


可选的 **InputSize** 元素指定原始扫描介质的大小。

<a name="usage"></a>使用情况
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
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>MustHonor</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
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

**InputSize** 元素可包含 [**DocumentSizeAutoDetect**](documentsizeautodetect.md)或 [**InputMediaSize**](inputmediasize.md)元素，但不能同时包含两者。 **DocumentSizeAutoDetect** 指定设备 u) 检测原始页面的大小。 **InputMediaSize** 指定要为当前作业扫描的媒体的大小。

仅当 **InputSize** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**DocumentSizeAutoDetect**](documentsizeautodetect.md)

[**InputMediaSize**](inputmediasize.md)

 

 






