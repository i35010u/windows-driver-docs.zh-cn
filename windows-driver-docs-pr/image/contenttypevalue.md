---
title: ContentTypeValue 元素
description: 所需的 ContentTypeValue 元素指定扫描设备支持的一种文档内容类型。
ms.assetid: 04d29626-cc14-4db3-88ec-cfb1cc9cd1cd
keywords:
- ContentTypeValue 元素成像设备
topic_type:
- apiref
api_name:
- wscn ContentTypeValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e8190515e51182546dda1c6013d0b551940fb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522657"
---
# <a name="contenttypevalue-element"></a>ContentTypeValue 元素


所需**ContentTypeValue**元素指定扫描设备支持的一种文档内容类型。

<a name="usage"></a>用法
-----

```xml
<wscn:ContentTypeValue>
  text
</wscn:ContentTypeValue>
```

<a name="attributes"></a>属性
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
<td><p><span id="Auto_"></span><span id="auto_"></span><span id="AUTO_"></span>Auto</p></td>
<td><p>设备会自动检测原始文档类型。</p></td>
</tr>
<tr class="even">
<td><p><span id="Text_"></span><span id="text_"></span><span id="TEXT_"></span>Text</p></td>
<td><p>原始文档主要组成不同的文本背景的强形成鲜明对比。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Photo_"></span><span id="photo_"></span><span id="PHOTO_"></span>Photo</p></td>
<td><p>原始文档主要组成摄影图像，其中灰度梯度逐渐更改和边缘并不是截然不同。</p></td>
</tr>
<tr class="even">
<td><p><span id="Halftone_"></span><span id="halftone_"></span><span id="HALFTONE_"></span>半色调</p></td>
<td><p>原始主要组成半色调映像。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Mixed_"></span><span id="mixed_"></span><span id="MIXED_"></span>混合</p></td>
<td><p>原始文档是具有多个特定文档内容类型的特征的多页文档。</p></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有子元素。

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

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>另请参阅


[**ContentTypesSupported**](contenttypessupported.md)

 

 






