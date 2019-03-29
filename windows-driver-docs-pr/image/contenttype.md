---
title: ContentType 元素
description: 可选的 ContentType 元素指定了原始文档的主要特征。
ms.assetid: 0e91e4ec-5569-452f-b929-9d2923f3147d
keywords:
- ContentType 元素成像设备
topic_type:
- apiref
api_name:
- wscn ContentType wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 716d82d6fdfae30d3be268f50c5620954837697d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575680"
---
# <a name="contenttype-element"></a>ContentType 元素


可选**ContentType**元素指定了原始文档的主要特征。

<a name="usage"></a>用法
-----

```xml
<wscn:ContentType wscn:MustHonor=""                  wscn:Override=""                  wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ContentType wscn:MustHonor=""                  wscn:Override=""                  wscn:UsedDefault="">
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
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。</p></td>
</tr>
<tr class="even">
<td><p><strong><strong>Override</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。</p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。</p></td>
</tr>
</tbody>
</table>

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
<td><p><span id="Auto"></span><span id="auto"></span><span id="AUTO"></span>Auto</p></td>
<td><p>扫描设备会自动检测原始类型。</p></td>
</tr>
<tr class="even">
<td><p><span id="Text"></span><span id="text"></span><span id="TEXT"></span>Text</p></td>
<td><p>该文档主要组成不同的文本背景的强形成鲜明对比。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Photo"></span><span id="photo"></span><span id="PHOTO"></span>Photo</p></td>
<td><p>原始主要组成摄影图像，其中灰度梯度逐渐更改和边缘并不是截然不同。</p></td>
</tr>
<tr class="even">
<td><p><span id="Halftone"></span><span id="halftone"></span><span id="HALFTONE"></span>半色调</p></td>
<td><p>原始主要组成半色调映像。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Mixed"></span><span id="mixed"></span><span id="MIXED"></span>混合</p></td>
<td><p>具有多个特定文档类型的特征的多页文档。</p></td>
</tr>
</tbody>
</table>

 

您都可以扩展和元素的值的子集。

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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端可以指定可选**MustHonor**属性时，才**ContentType**元素包含在**CreateScanJobRequest**层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅[ **CreateScanJobRequest**](createscanjobrequest.md)。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**ContentType**元素包含在**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

 

 






