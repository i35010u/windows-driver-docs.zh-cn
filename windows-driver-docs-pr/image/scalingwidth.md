---
title: ScalingWidth 元素
description: 所需的 ScalingWidth 元素指定快速扫描方向缩放的文档。
ms.assetid: 5bc7cec8-888a-4b95-9593-94e6e23777bf
keywords:
- ScalingWidth 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScalingWidth wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2f4ac218098b32023e064f9596bbf5d1808642b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364397"
---
# <a name="scalingwidth-element"></a>ScalingWidth 元素


所需**ScalingWidth**元素指定快速扫描方向缩放的文档。

<a name="usage"></a>用法
-----

```xml
<wscn:ScalingWidth wscn:Override=""                   wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:ScalingWidth wscn:Override=""                   wscn:UsedDefault="">
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
<td><p><strong><strong>Override</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 一个布尔值，必须为 0，为 false，1 或 true。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
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

必需。 从 1 到 1000，（含) 范围内的整数。

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
<td><p><a href="scaling.md" data-raw-source="[&lt;strong&gt;Scaling&lt;/strong&gt;](scaling.md)"><strong>缩放</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScalingWidth**元素指定要应用中快速扫描方向的缩放系数。 缩放以 1%的增量，其中的值为 100 表示 100%的宽度横向 （不到文档的宽度调整） 表示。

所有 WSD 扫描服务必须至少都支持值 100。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**ScalingWidth**元素包含在**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

你可以部分为此元素允许的值。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**缩放**](scaling.md)

[**ScalingHeight**](scalingheight.md)

 

 






