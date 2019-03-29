---
title: 对比度元素
description: 可选的对比度元素指定的相对量，以减少或增强的对比度扫描的文档。
ms.assetid: c40e824f-4e10-4590-a524-ff69a21a4499
keywords:
- 对比度元素成像设备
topic_type:
- apiref
api_name:
- wscn Contrast wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09ce7469fdffcb588e122929e669287297204f5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566280"
---
# <a name="contrast-element"></a>对比度元素


可选**对比度**元素指定的相对量，以减少或增强的对比度扫描的文档。

<a name="usage"></a>用法
-----

```xml
<wscn:Contrast wscn:Override="" wscn:UsedDefault=""
  Override = "xs:string"
  UsedDefault = "xs:string">
  text
</wscn:Contrast wscn:Override="" wscn:UsedDefault="">
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

对比度值必须为-1000 到 1000 之间 （含） 范围内。

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

**对比度**元素指示的相对量，以增强或降低扫描的文档的对比度。 值为 0 指示 WSD 扫描服务应进行任何调整扫描生成的对比度。

所有 WSD 扫描服务必须都支持的所有值之间，其中包含，-1000 到 1000年。 服务必须在内部将这些值映射到的实际**对比度**扫描设备支持的值。

WSD 扫描服务可以指定可选**重写**并**UsedDefault**属性时，才**对比度**元素包含在**DocumentFinalParameters**层次结构。 有关详细信息**重写**并**UsedDefault**及其使用情况，请参阅[ **DocumentFinalParameters**](documentfinalparameters.md)。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






