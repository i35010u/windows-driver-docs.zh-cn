---
title: DeviceSettings 元素
description: 所需的 DeviceSettings 元素描述扫描设备的基本功能。
ms.assetid: d12d25f0-fa94-4840-bb1a-cc1a5352767c
keywords:
- DeviceSettings 元素成像设备
topic_type:
- apiref
api_name:
- wscn DeviceSettings
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9c36595743fb3004ba75f143e447496d8c421df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364549"
---
# <a name="devicesettings-element"></a>DeviceSettings 元素


所需**DeviceSettings**元素描述扫描设备的基本功能。

<a name="usage"></a>用法
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

**DeviceSettings**元素包含支持的值可以设置中的图像处理选项的许多[ **ScanTicket** ](scanticket.md)扫描操作的元素。 客户端可以使用中返回的值**DeviceSettings**若要创建有效**ScanTicket**元素。

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

 

 






