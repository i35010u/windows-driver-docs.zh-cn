---
title: MediaSides 元素
description: 可选的 MediaSides 元素包含扫描媒体的每个物理端的唯一参数。
keywords:
- MediaSides 元素图像设备
topic_type:
- apiref
api_name:
- wscn MediaSides wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f06ee31c638e50807a74e0c5a8819266cb8af1b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792249"
---
# <a name="mediasides-element"></a>MediaSides 元素


可选的 **MediaSides** 元素包含扫描媒体的每个物理端的唯一参数。

<a name="usage"></a>使用情况
-----

```xml
<wscn:MediaSides wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:MediaSides wscn:MustHonor="">
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
<td><p><a href="mediaback.md" data-raw-source="[&lt;strong&gt;MediaBack&lt;/strong&gt;](mediaback.md)"><strong>MediaBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
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

许多支持双工的扫描程序允许为扫描媒体的每个物理端设置不同的扫描区域、颜色处理和分辨率。 **MediaSides** 元素包含媒体正面和背面的单独数据。 每个扫描作业都可以包含媒体前面的参数。

仅当扫描程序支持双工扫描且当前 [**InputSource**](inputsource.md)为 **ADFDuplex** 时， [**MediaBack**](mediaback.md)元素才有效。

如果 **InputSource** 为 **ADFDuplex** ，并且缺少 **MediaBack** 元素，则在 **MediaFront** 中指定的所有参数也会应用于后端扫描。

仅当 **MediaSides** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

仅当 **MediaSides** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定可选 **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**InputSource**](inputsource.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

 

 






