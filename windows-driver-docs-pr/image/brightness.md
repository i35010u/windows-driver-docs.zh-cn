---
title: 亮度元素
description: 可选亮度元素指定要减少或增强扫描文档亮度的相对量。
keywords:
- 亮度元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Brightness wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362061f27b2c2d1accc2d77bbcf2cae7e0b23760
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816241"
---
# <a name="brightness-element"></a>亮度元素


可选 **亮度** 元素指定要减少或增强扫描文档亮度的相对量。

<a name="usage"></a>使用情况
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

亮度值必须介于-1000 到1000（含）之间。**亮度**

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

**亮度** 元素指示要减少或增强扫描文档亮度的相对量。 如果值为0，则表示 WSD 扫描服务对扫描的亮度不做任何调整。

所有 WSD 扫描服务都必须支持从、-1000 到1000的所有值。 服务必须在内部将这些值映射到扫描设备支持的实际 **亮度** 值。

仅当 **亮度** 元素包含在 [**DocumentFinalParameters**](documentfinalparameters.md)层次结构中时，WSD 扫描服务才能指定可选 **Override** 和 **UsedDefault** 属性。 有关 **Override** 和 **UsedDefault** 及其用法的详细信息，请参阅 **DocumentFinalParameters**。

可以将 **亮度** 元素的允许值作为子集。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**ExposureSettings**](exposuresettings.md)

 

 






