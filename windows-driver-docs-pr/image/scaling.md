---
title: 缩放元素
description: 可选缩放元素指定扫描文档的宽度和高度的缩放。
keywords:
- 缩放元素图像设备
topic_type:
- apiref
api_name:
- wscn Scaling wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39e661dcfe9d757ffdb5afa159ca6c85f082e2c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822395"
---
# <a name="scaling-element"></a>缩放元素


可选 **缩放** 元素指定扫描文档的宽度和高度的缩放。

<a name="usage"></a>使用情况
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

**缩放** 元素必须同时包含 [**ScalingWidth**](scalingwidth.md)和 [**ScalingHeight**](scalingheight.md)元素。 **ScalingWidth** 元素按快速扫描方向指定缩放， **ScalingHeight** 元素以慢速扫描方向指定缩放。

仅当 **缩放** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**ScalingHeight**](scalingheight.md)

[**ScalingWidth**](scalingwidth.md)

 

 






