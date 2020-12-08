---
title: 解析元素
description: 可选的解决方法元素指定扫描图像的分辨率。
keywords:
- 解析元素图像设备
topic_type:
- apiref
api_name:
- wscn Resolution wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8c3386a9889f222136ff97f40d887240aa40e1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814411"
---
# <a name="resolution-element"></a>解析元素


可选的 **解决方法** 元素指定扫描图像的分辨率。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Resolution wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:Resolution wscn:MustHonor="">
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>高度</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>宽度</strong></a></p></td>
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
<td><p><a href="mediaback.md" data-raw-source="[&lt;strong&gt;MediaBack&lt;/strong&gt;](mediaback.md)"><strong>MediaBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**解析** 元素包含用于描述所需的扫描分辨率的单一 [**宽度**](width.md)x [**高度**](height.md)对。 如果缺少 **Height** 元素，则使用 **Width** 值，从而生成正方形解析 (例如 300 x 300) 。

**分辨率** 值以像素/英寸为单位。

仅当 **解析** 元素包含在 **CreateScanJobRequest** 层次结构内时，客户端才能指定可选的 **MustHonor** 属性。 有关 **MustHonor** 及其用法的详细信息，请参阅 [**CreateScanJobRequest**](createscanjobrequest.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**高度**](height.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

[**宽度**](width.md)

 

 






