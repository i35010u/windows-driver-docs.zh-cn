---
title: DeviceSettings 元素
description: 必需的 DeviceSettings 元素描述扫描设备的基本功能。
keywords:
- DeviceSettings 元素图像设备
topic_type:
- apiref
api_name:
- wscn DeviceSettings
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dedae53b3f8586d6d75d3c0490f3605f1cf628d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833511"
---
# <a name="devicesettings-element"></a>DeviceSettings 元素


必需的 **DeviceSettings** 元素描述扫描设备的基本功能。

<a name="usage"></a>使用情况
-----

```xml
<wscn:DeviceSettings>
  child elements
</wscn:DeviceSettings>
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
<td><p><a href="autoexposuresupported.md" data-raw-source="[&lt;strong&gt;AutoExposureSupported&lt;/strong&gt;](autoexposuresupported.md)"><strong>AutoExposureSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="brightnesssupported.md" data-raw-source="[&lt;strong&gt;BrightnessSupported&lt;/strong&gt;](brightnesssupported.md)"><strong>BrightnessSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="compressionqualityfactorsupported.md" data-raw-source="[&lt;strong&gt;CompressionQualityFactorSupported&lt;/strong&gt;](compressionqualityfactorsupported.md)"><strong>CompressionQualityFactorSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="contenttypessupported.md" data-raw-source="[&lt;strong&gt;ContentTypesSupported&lt;/strong&gt;](contenttypessupported.md)"><strong>ContentTypesSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="contrastsupported.md" data-raw-source="[&lt;strong&gt;ContrastSupported&lt;/strong&gt;](contrastsupported.md)"><strong>ContrastSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentsizeautodetectsupported.md" data-raw-source="[&lt;strong&gt;DocumentSizeAutoDetectSupported&lt;/strong&gt;](documentsizeautodetectsupported.md)"><strong>DocumentSizeAutoDetectSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="formatssupported.md" data-raw-source="[&lt;strong&gt;FormatsSupported&lt;/strong&gt;](formatssupported.md)"><strong>FormatsSupported</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="rotationssupported.md" data-raw-source="[&lt;strong&gt;RotationsSupported&lt;/strong&gt;](rotationssupported.md)"><strong>RotationsSupported</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scalingrangesupported.md" data-raw-source="[&lt;strong&gt;ScalingRangeSupported&lt;/strong&gt;](scalingrangesupported.md)"><strong>ScalingRangeSupported</strong></a></p></td>
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
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**DeviceSettings** 元素包含多个可在 [**ScanTicket**](scanticket.md)元素中为扫描操作设置的支持的值。 客户端可以使用 **DeviceSettings** 中返回的值来创建有效的 **ScanTicket** 元素。

## <a name="see-also"></a>请参阅


[**AutoExposureSupported**](autoexposuresupported.md)

[**BrightnessSupported**](brightnesssupported.md)

[**CompressionQualityFactorSupported**](compressionqualityfactorsupported.md)

[**ContentTypesSupported**](contenttypessupported.md)

[**ContrastSupported**](contrastsupported.md)

[**DocumentSizeAutoDetectSupported**](documentsizeautodetectsupported.md)

[**FormatsSupported**](formatssupported.md)

[**RotationsSupported**](rotationssupported.md)

[**ScalingRangeSupported**](scalingrangesupported.md)

[**ScanTicket**](scanticket.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






