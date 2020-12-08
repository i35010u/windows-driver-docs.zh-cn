---
title: CompressionQualityFactorSupported 元素
description: 必需的 CompressionQualityFactorSupported 元素指定扫描设备支持的压缩质量系数的范围。
keywords:
- CompressionQualityFactorSupported 元素图像设备
topic_type:
- apiref
api_name:
- wscn CompressionQualityFactorSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5833e9ab1ada001fcd39d796b102cedab7639633
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783915"
---
# <a name="compressionqualityfactorsupported-element"></a>CompressionQualityFactorSupported 元素


必需的 **CompressionQualityFactorSupported** 元素指定扫描设备支持的压缩质量系数的范围。

<a name="usage"></a>使用情况
-----

```xml
<wscn:CompressionQualityFactorSupported>
  child elements
</wscn:CompressionQualityFactorSupported>
```

<a name="attributes"></a>特性
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
<td><p><a href="maxvalue.md" data-raw-source="[&lt;strong&gt;MaxValue&lt;/strong&gt;](maxvalue.md)"><strong>Timespan.maxvalue</strong></a></p></td>
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

压缩质量因素是一个整数值，用于有损压缩类型，以确定压缩期间可接受的图像丢失量。 请求的保真度越大，生成的文件大小就越大。

[**MinValue**](minvalue.md)[**MaxValue**](maxvalue.md)

扫描设备支持的最小和最大压缩质量因素分别在 MinValue 和 [**MinValue**](minvalue.md)元素 [**中**](maxvalue.md)指定。 **MinValue** 和 **MaxValue** 必须是从1到100的整数。 值100表示设备应该使用它所支持的最小压缩量来生成最高质量的映像。 目前，JPEG 压缩是唯一受支持的有损压缩类型。

## <a name="see-also"></a>请参阅


[**DeviceSettings**](devicesettings.md)

[**Timespan.maxvalue**](maxvalue.md)

[**MinValue**](minvalue.md)

 

 






