---
title: ScalingWidth 元素
description: 必需的 ScalingWidth 元素包含范围的允许值为缩放输出文档的宽度。
ms.assetid: 8b15f4b9-8537-479e-8745-0c8b35883bf5
keywords:
- ScalingWidth 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScalingWidth
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 042c342380510624166107a867d23d8d7f3a6cbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519434"
---
# <a name="scalingwidth-element"></a>ScalingWidth 元素


所需**ScalingWidth**元素包含范围的允许值为缩放输出文档的宽度。

<a name="usage"></a>用法
-----

```xml
<wscn:ScalingWidth>
  child elements
</wscn:ScalingWidth>
```

<a name="attributes"></a>属性
----------

没有特性。

## <a name="child-elements"></a>子元素


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
<td><p><a href="maxvalue.md" data-raw-source="[&lt;strong&gt;MaxValue&lt;/strong&gt;](maxvalue.md)"><strong>MaxValue</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="minvalue.md" data-raw-source="[&lt;strong&gt;MinValue&lt;/strong&gt;](minvalue.md)"><strong>MinValue</strong></a></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="scalingrangesupported.md" data-raw-source="[&lt;strong&gt;ScalingRangeSupported&lt;/strong&gt;](scalingrangesupported.md)"><strong>ScalingRangeSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScalingWidth**元素包含[ **MinValue** ](minvalue.md)并[ **MaxValue** ](maxvalue.md)指定的元素扫描设备支持缩放宽度的输出文档的最小和最大值。

**MinValue**并**MaxValue**必须是介于 1 到 1000，整数**MinValue**小于或等于**MaxValue**。 值为 100 表示扫描设备不应进行的扫描图像宽度调整。 至少，WSD 扫描服务必须支持值为 100。

## <a name="see-also"></a>另请参阅


[**MaxValue**](maxvalue.md)

[**MinValue**](minvalue.md)

[**ScalingHeight**](scalingheight2.md)

[**ScalingRangeSupported**](scalingrangesupported.md)

 

 






