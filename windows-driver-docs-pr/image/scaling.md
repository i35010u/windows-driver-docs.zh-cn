---
title: 缩放元素
description: 可选的缩放元素指定宽度和高度的扫描的文档的缩放。
ms.assetid: 43769ebf-f883-418a-a0b3-87d5b23601f9
keywords:
- 缩放元素成像设备
topic_type:
- apiref
api_name:
- wscn Scaling wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7791a9ab6be968766e2fa873c5ee233758809d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381547"
---
# <a name="scaling-element"></a>缩放元素


可选**缩放**元素指定宽度和高度的扫描的文档的缩放。

<a name="usage"></a>用法
-----

```xml
<wscn:Scaling wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:Scaling wscn:MustHonor="">
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
<td><p><a href="scalingheight.md" data-raw-source="[&lt;strong&gt;ScalingHeight&lt;/strong&gt;](scalingheight.md)"><strong>ScalingHeight</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scalingwidth.md" data-raw-source="[&lt;strong&gt;ScalingWidth&lt;/strong&gt;](scalingwidth.md)"><strong>ScalingWidth</strong></a></p></td>
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

**缩放**元素必须同时包含[ **ScalingWidth** ](scalingwidth.md)并[ **ScalingHeight** ](scalingheight.md)元素。 **ScalingWidth**元素指定快速扫描方向的缩放和**ScalingHeight**元素指定在进行慢扫描方向的缩放。

客户端可以指定可选**MustHonor**属性时，才**缩放**元素包含在**CreateScanJobRequest**层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅[ **CreateScanJobRequest**](createscanjobrequest.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**ScalingHeight**](scalingheight.md)

[**ScalingWidth**](scalingwidth.md)

 

 






