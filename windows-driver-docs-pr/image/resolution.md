---
title: 解析元素
description: 可选的解析元素指定扫描图像的分辨率。
ms.assetid: d46c197d-40ed-4623-a842-7ee5cb9e8367
keywords:
- 解析元素成像设备
topic_type:
- apiref
api_name:
- wscn Resolution wscn MustHonor ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 255336081378ac86b22aeb48fdc150d1cc01089d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525166"
---
# <a name="resolution-element"></a>解析元素


可选**解析**元素指定扫描图像的分辨率。

<a name="usage"></a>用法
-----

```xml
<wscn:Resolution wscn:MustHonor=""
  MustHonor = "xs:string">
  child elements
</wscn:Resolution wscn:MustHonor="">
```

<a name="attributes"></a>属性
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>Height</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>Width</strong></a></p></td>
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

**解析**元素包含一个[**宽度**](width.md) x [**高度**](height.md)描述对所需的扫描分辨率。 如果**高度**元素缺少**宽度**使用值，无法完成方形的解决方法 (例如，300x300)。

**解析**值均以每英寸像素数。

客户端可以指定可选**MustHonor**属性时，才**解析**元素包含在**CreateScanJobRequest**层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅[ **CreateScanJobRequest**](createscanjobrequest.md)。

## <a name="see-also"></a>另请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**Height**](height.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

[**Width**](width.md)

 

 






