---
title: MediaSides 元素
description: 可选 MediaSides 元素包含是唯一的每个物理扫描媒体一端的参数。
ms.assetid: 9bd3de21-4b2c-4cea-add6-51240ad6c19f
keywords:
- MediaSides 元素成像设备
topic_type:
- apiref
api_name:
- wscn MediaSides wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 270514ab08bfc3d0461919d0814935ac7ea5450c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379685"
---
# <a name="mediasides-element"></a>MediaSides 元素


可选**MediaSides**元素包含是唯一的每个物理扫描媒体一端的参数。

<a name="usage"></a>用法
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

许多双工能力的扫描程序允许设置不同的扫描区域、 颜色处理和每个物理扫描媒体一端的解决方法。 **MediaSides**元素包含的媒体的前端和后端边单独的数据。 每个扫描作业可以有媒体前面的参数。

[ **MediaBack** ](mediaback.md)元素是有效的扫描程序仅从时支持双工扫描和当前[ **InputSource** ](inputsource.md)是**ADFDuplex**。

如果**InputSource**是**ADFDuplex**并**MediaBack**缺少元素，在中指定的所有参数**MediaFront**将适用于扫描以及在后端。

客户端可以指定可选**MustHonor**属性时，才**MediaSides**元素包含在**CreateScanJobRequest**层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅[ **CreateScanJobRequest**](createscanjobrequest.md)。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**MediaSides**元素包含在**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**InputSource**](inputsource.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

 

 






