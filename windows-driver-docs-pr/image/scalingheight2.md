---
title: ScalingHeight 元素
description: 所需的 ScalingHeight 元素包含范围的允许值为缩放输出文档的高度。
ms.assetid: f13e1ef8-e05f-4aab-bf2a-08a953638334
keywords:
- ScalingHeight 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScalingHeight
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ad54a20b497e2fed139a5a0c78af2f681c468a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519432"
---
# <a name="scalingheight-element"></a>ScalingHeight 元素


所需**ScalingHeight**元素包含范围的允许值为缩放输出文档的高度。

<a name="usage"></a>用法
-----

```xml
<wscn:ScalingHeight>
  child elements
</wscn:ScalingHeight>
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

**ScalingHeight**元素包含[ **MinValue** ](minvalue.md)并[ **MaxValue** ](maxvalue.md)元素，指定用于缩放的输出文档的高度支持扫描设备的最小值和最大值。

**MinValue**并**MaxValue**必须是介于 1 到 1000，整数**MinValue**小于或等于**MaxValue**。 扫描设备不应进行的扫描图像的高度调整 100 表示的值。 至少，WSD 扫描服务必须支持值为 100。

## <a name="see-also"></a>另请参阅


[**MaxValue**](maxvalue.md)

[**MinValue**](minvalue.md)

[**ScalingRangeSupported**](scalingrangesupported.md)

[**ScalingWidth2**](scalingwidth.md)

 

 






