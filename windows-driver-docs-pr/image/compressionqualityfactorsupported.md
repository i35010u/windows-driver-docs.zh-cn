---
title: CompressionQualityFactorSupported 元素
description: 所需的 CompressionQualityFactorSupported 元素指定扫描设备支持的压缩质量因素的范围。
ms.assetid: f82ae450-b948-463e-a6a8-aaea0575ddb9
keywords:
- CompressionQualityFactorSupported 元素成像设备
topic_type:
- apiref
api_name:
- wscn CompressionQualityFactorSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad865665dd74739d47577916b8ad33eb228fa393
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525347"
---
# <a name="compressionqualityfactorsupported-element"></a>CompressionQualityFactorSupported 元素


所需**CompressionQualityFactorSupported**元素指定扫描设备支持的压缩质量因素的范围。

<a name="usage"></a>用法
-----

```xml
<wscn:CompressionQualityFactorSupported>
  child elements
</wscn:CompressionQualityFactorSupported>
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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

压缩质量因素是一个整数值，用于有损压缩类型，以在压缩过程确定可接受映像丢失量。 越大生成的文件大小将为请求的保真度更高版本。

[**MinValue**](minvalue.md)[**MaxValue**](maxvalue.md)

中指定扫描设备支持的最小值和最大的压缩质量因素[ **MinValue** ](minvalue.md)并[ **MaxValue** ](maxvalue.md)元素，分别。 **MinValue**并**MaxValue**必须是 1 到 100 之间的整数。 值为 100 表示设备应使用最少量的压缩该解决方案还支持以生成最高质量的图像。 目前，JPEG 压缩是唯一受支持的有损压缩类型。

## <a name="see-also"></a>另请参阅


[**DeviceSettings**](devicesettings.md)

[**MaxValue**](maxvalue.md)

[**MinValue**](minvalue.md)

 

 






