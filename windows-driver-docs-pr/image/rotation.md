---
title: 旋转元素
description: 可选的旋转元素指定扫描文档的每个图像的旋转量。
keywords:
- 旋转元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Rotation wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c136818d2be69d3ccceaea875cc8adf1d7127f11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790619"
---
# <a name="rotation-element"></a>旋转元素


可选的 **旋转** 元素指定扫描文档的每个图像的旋转量。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Rotation wscn:MustHonor=""               wscn:Override=""               wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Rotation wscn:MustHonor=""               wscn:Override=""               wscn:UsedDefault="">
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
<tr class="even">
<td><p><strong><strong>忽略</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

必需。 0、90、180或270之一。

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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**旋转** 元素的整数值指定要应用于扫描文档的每个图像的顺时针旋转。 所有 WSD 扫描服务都必须支持值 0 (即无旋转) 。

仅当 **旋转** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

仅当 **旋转** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才可以指定可选 **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






