---
title: MinValue 元素
description: 必需的 MinValue 元素指定扫描设备对需要一系列值的扫描程序配置元素所支持的最小值。
keywords:
- MinValue 元素图像设备
topic_type:
- apiref
api_name:
- wscn MinValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcab39dd61083d25f9664a598cc426a88348a000
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827139"
---
# <a name="minvalue-element"></a>MinValue 元素


必需的 **MinValue** 元素指定扫描设备对需要一系列值的扫描程序配置元素所支持的最小值。

<a name="usage"></a>使用情况
-----

```xml
<wscn:MinValue>
  text
</wscn:MinValue>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 有关可能的值，请参阅特定父元素。

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
<td><p><a href="compressionqualityfactorsupported.md" data-raw-source="[&lt;strong&gt;CompressionQualityFactorSupported&lt;/strong&gt;](compressionqualityfactorsupported.md)"><strong>CompressionQualityFactorSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scalingheight2.md" data-raw-source="[&lt;strong&gt;ScalingHeight&lt;/strong&gt;](scalingheight2.md)"><strong>ScalingHeight</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scalingwidth2.md" data-raw-source="[&lt;strong&gt;ScalingWidth&lt;/strong&gt;](scalingwidth2.md)"><strong>ScalingWidth</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**MinValue** 元素的值取决于其父元素。 有关可能的值，请参阅相应的父元素。

## <a name="see-also"></a>请参阅


[**CompressionQualityFactorSupported**](compressionqualityfactorsupported.md)

[**Timespan.maxvalue**](maxvalue.md)

[**ScalingHeight**](scalingheight2.md)

[**ScalingWidth**](scalingwidth2.md)

 

 






