---
title: 清晰度元素
description: 可选的清晰度元素指定的相对量，以减少或增强的清晰度的扫描的文档。
ms.assetid: 80a2023e-74fa-4e7e-b8e7-ecae8827cf5b
keywords:
- 清晰度元素成像设备
topic_type:
- apiref
api_name:
- wscn Sharpness wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f28fa4e62977f79ff3c7666c4afd79131737f4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367889"
---
# <a name="sharpness-element"></a>清晰度元素


可选**清晰度**元素指定的相对量，以减少或增强的清晰度的扫描的文档。

<a name="usage"></a>用法
-----

```xml
<wscn:Sharpness wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Sharpness wscn:Override="" wscn:UsedDefault="">
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

从通过 100 (含)-100 的范围中的值。

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
<td><p><a href="exposuresettings.md" data-raw-source="[&lt;strong&gt;ExposureSettings&lt;/strong&gt;](exposuresettings.md)"><strong>ExposureSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**清晰度**元素指示要减少或增强的清晰度的扫描的文档的相对量。 值为 0 指示 WSD 扫描服务应进行任何调整扫描和清晰度等等。

扫描的所有服务必须至少都支持值 0。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**清晰度**元素包含在**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

你可以部分为此元素允许的值。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






