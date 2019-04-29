---
title: 亮度元素
description: 可选的亮度元素指定的相对量，以减少或增强扫描的文档的亮度。
ms.assetid: 15b1b9a1-4735-4a25-837e-8fd9e9ecf88d
keywords:
- 亮度元素成像设备
topic_type:
- apiref
api_name:
- wscn Brightness wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a8f7e845e54a8156d8ede79f74f842fb0ac1ba0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373313"
---
# <a name="brightness-element"></a>亮度元素


可选**亮度**元素指定的相对量，以减少或增强扫描的文档的亮度。

<a name="usage"></a>用法
-----

```xml
<wscn:Brightness wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Brightness wscn:Override="" wscn:UsedDefault="">
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

亮度值必须为-1000 到 1000 之间 （含） 范围内。**亮度**

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

**亮度**元素指示的相对量，以减少或增强扫描的文档的亮度。 值为 0 指示 WSD 扫描服务应进行任何调整扫描亮度。

所有 WSD 扫描服务必须都支持从和包括的所有值为-1000 到 1000 之间。 服务必须在内部将这些值映射到的实际**亮度**扫描设备支持的值。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**亮度**元素包含在[ **DocumentFinalParameters** ](documentfinalparameters.md)层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅**DocumentFinalParameters**。

你可以子集的允许的值为**亮度**元素。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






