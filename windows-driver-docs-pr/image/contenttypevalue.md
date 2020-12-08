---
title: ContentTypeValue 元素
description: 必需的 ContentTypeValue 元素指定扫描设备支持的一个文档内容类型。
keywords:
- ContentTypeValue 元素图像设备
topic_type:
- apiref
api_name:
- wscn ContentTypeValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419c2bd9aa0e8ddf70140069dc69f299ba97f771
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831813"
---
# <a name="contenttypevalue-element"></a>ContentTypeValue 元素


必需的 **ContentTypeValue** 元素指定扫描设备支持的一个文档内容类型。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ContentTypeValue>
  text
</wscn:ContentTypeValue>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="Auto_"></span><span id="auto_"></span><span id="AUTO_"></span>自动</p></td>
<td><p>设备将自动检测原始文档类型。</p></td>
</tr>
<tr class="even">
<td><p><span id="Text_"></span><span id="text_"></span><span id="TEXT_"></span>全文</p></td>
<td><p>原始文档主要由不同的文本组成，这与背景对比强烈。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Photo_"></span><span id="photo_"></span><span id="PHOTO_"></span>926</p></td>
<td><p>原始文档主要由照片图像组成，其中的阴影变化逐渐增加，边缘并不明显。</p></td>
</tr>
<tr class="even">
<td><p><span id="Halftone_"></span><span id="halftone_"></span><span id="HALFTONE_"></span>色</p></td>
<td><p>原始的主要包括 halftoned 映像。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Mixed_"></span><span id="mixed_"></span><span id="MIXED_"></span>混</p></td>
<td><p>原始文档是包含多个特定文档内容类型特征的多页文档。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="contenttypessupported.md" data-raw-source="[&lt;strong&gt;ContentTypesSupported&lt;/strong&gt;](contenttypessupported.md)"><strong>ContentTypesSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**ContentTypesSupported**](contenttypessupported.md)

 

 






