---
title: ColorProcessing 元素
description: 可选的 ColorProcessing 元素上扫描程序指定的输入源的颜色处理模式。
ms.assetid: 10170090-d0d2-44b1-bd0d-3b800669f7cf
keywords:
- ColorProcessing 元素成像设备
topic_type:
- apiref
api_name:
- wscn ColorProcessing wscn MustHonor "" wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1775e893213420118465aa11df7240c56177c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534866"
---
# <a name="colorprocessing-element"></a>ColorProcessing 元素


可选**ColorProcessing**元素上扫描程序指定的输入源的颜色处理模式。

<a name="usage"></a>用法
-----

```xml
<wscn:ColorProcessing wscn:MustHonor=""                      wscn:Override=""                      wscn:UsedDefault=""
  MustHonor = "xs:string"
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ColorProcessing wscn:MustHonor=""                      wscn:Override=""                      wscn:UsedDefault="">
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
<tr class="even">
<td><p><strong><strong>Override</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。<strong>falsetrue</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

有关列表和处理模式下的颜色的说明，请参阅 ColorEntry。[ **ColorEntry**](colorentry.md)

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
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端可以指定可选**MustHonor**属性时，才**ColorProcessing**元素包含在[ **CreateScanJobRequest**](createscanjobrequest.md)层次结构。 有关详细信息**MustHonor**及其使用情况，请参阅**CreateScanJobRequest**。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**ColorProcessing**元素包含在[**DocumentFinalParameters** ](documentfinalparameters.md)层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅**DocumentFinalParameters**。

## <a name="see-also"></a>另请参阅


[**ColorEntry**](colorentry.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**MediaFront**](mediafront.md)

 

 






