---
title: 清晰度元素
description: 可选的清晰度元素指定要减小或增强扫描文档的清晰度的相对量。
keywords:
- 清晰度元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Sharpness wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55231b8fe78220de597a95bd74660b74c61963d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830487"
---
# <a name="sharpness-element"></a>清晰度元素


可选的 **清晰度** 元素指定要减小或增强扫描文档的清晰度的相对量。

<a name="usage"></a>使用情况
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
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>忽略</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
<tr class="even">
<td><p><strong><strong>UsedDefault</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>可选。 必须为0、false、1或 true 的布尔值。<strong>falsetrue</strong></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

范围从-100 到100（含）之间的值。

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
<td><p><a href="exposuresettings.md" data-raw-source="[&lt;strong&gt;ExposureSettings&lt;/strong&gt;](exposuresettings.md)"><strong>ExposureSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**清晰度** 元素指示要减少或增强扫描文档的清晰度的相对量。 值0表示 WSD 扫描服务不应对扫描的清晰度进行调整。

所有扫描服务必须至少支持值0。

仅当 **锐度** 元素包含在 **DocumentFinalParameters** 层次结构中时，WSD 扫描服务才能指定 optional **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 [**DocumentFinalParameters**](documentfinalparameters.md)。

可以将此元素的允许值作为子集。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






