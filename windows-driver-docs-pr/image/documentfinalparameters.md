---
title: DocumentFinalParameters 元素
description: 所需的 DocumentFinalParameters 元素包含用于图像采集扫描设备的实际 DocumentParameters 元素。
ms.assetid: 54e3c96c-70a1-48c5-8718-45b0a71ff9b1
keywords:
- DocumentFinalParameters 元素成像设备
topic_type:
- apiref
api_name:
- wscn DocumentFinalParameters
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1771074892d19dbfb3fecbb0c51622b9c52b8d41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364542"
---
# <a name="documentfinalparameters-element"></a>DocumentFinalParameters 元素


所需**DocumentFinalParameters**元素包含的实际[ **DocumentParameters** ](documentparameters.md)扫描设备使用的图像采集的元素。

<a name="usage"></a>用法
-----

```xml
<wscn:DocumentFinalParameters>
  child elements
</wscn:DocumentFinalParameters>
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
<td><p><a href="compressionqualityfactor.md" data-raw-source="[&lt;strong&gt;CompressionQualityFactor&lt;/strong&gt;](compressionqualityfactor.md)"><strong>CompressionQualityFactor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="contenttype.md" data-raw-source="[&lt;strong&gt;ContentType&lt;/strong&gt;](contenttype.md)"><strong>ContentType</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="exposure.md" data-raw-source="[&lt;strong&gt;Exposure&lt;/strong&gt;](exposure.md)"><strong>风险</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="filmscanmode.md" data-raw-source="[&lt;strong&gt;FilmScanMode&lt;/strong&gt;](filmscanmode.md)"><strong>FilmScanMode</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="format.md" data-raw-source="[&lt;strong&gt;Format&lt;/strong&gt;](format.md)"><strong>Format</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="imagestotransfer.md" data-raw-source="[&lt;strong&gt;ImagesToTransfer&lt;/strong&gt;](imagestotransfer.md)"><strong>ImagesToTransfer</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="inputsize.md" data-raw-source="[&lt;strong&gt;InputSize&lt;/strong&gt;](inputsize.md)"><strong>InputSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="inputsource.md" data-raw-source="[&lt;strong&gt;InputSource&lt;/strong&gt;](inputsource.md)"><strong>InputSource</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="mediasides.md" data-raw-source="[&lt;strong&gt;MediaSides&lt;/strong&gt;](mediasides.md)"><strong>MediaSides</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="rotation.md" data-raw-source="[&lt;strong&gt;Rotation&lt;/strong&gt;](rotation.md)"><strong>旋转</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scaling.md" data-raw-source="[&lt;strong&gt;Scaling&lt;/strong&gt;](scaling.md)"><strong>缩放</strong></a></p></td>
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
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>文档</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**DocumentFinalParameters**元素包含包含 WSD 扫描服务使用的实际扫描作业值的元素。 这些值可能不同于在作业中请求的值[ **ScanTicket** ](scanticket.md)出于各种原因。 每个参数表示此层次结构中，值已知时必须填写。

中的某些元素**DocumentFinalParameters**层次结构可以包含**重写**并**UsedDefault**布尔值特性。 如果**重写**属性是否存在并且在一个元素，则返回 true，扫描设备重写了指定的值与请求的值。 如果**UsedDefault**属性是否存在并且在一个元素，则返回 true，扫描设备使用指定的默认值。

[**亮度**](brightness.md)[**ColorProcessing**](colorprocessing.md)[**CompressionQualityFactor** ](compressionqualityfactor.md) [**ContentType**](contenttype.md)[**对比度**](contrast.md)[**FilmScanMode** ](filmscanmode.md) [**格式**](format.md)[**高度**](height.md)[**ImagesToTransfer** ](imagestotransfer.md) [**InputSource**](inputsource.md)[**旋转**](rotation.md)[**ScalingHeight** ](scalingheight.md) [**ScalingWidth**](scalingwidth.md)[**ScanRegionHeight**](scanregionheight.md)[**ScanRegionWidth**](scanregionwidth.md) [ **ScanRegionXOffset**](scanregionxoffset.md)[**ScanRegionYOffset** ](scanregionyoffset.md) [**清晰度**](sharpness.md)[**宽度**](width.md)

下列元素可以具有**重写**并**UsedDefault**属性：[**亮度**](brightness.md)， [ **ColorProcessing**](colorprocessing.md)， [ **CompressionQualityFactor**](compressionqualityfactor.md)， [**ContentType**](contenttype.md)， [**对比度**](contrast.md)， [ **FilmScanMode**](filmscanmode.md)，[**格式**](format.md)， [**高度**](height.md)， [ **ImagesToTransfer** ](imagestotransfer.md)， [ **InputSource**](inputsource.md)， [**旋转**](rotation.md)， [ **ScalingHeight**](scalingheight.md)， [ **ScalingWidth**](scalingwidth.md)， [ **ScanRegionHeight**](scanregionheight.md)， [ **ScanRegionWidth**](scanregionwidth.md)， [ **ScanRegionXOffset**](scanregionxoffset.md)， [ **ScanRegionYOffset** ](scanregionyoffset.md)， [**清晰度**](sharpness.md)，和[**宽度**](width.md)。

## <a name="see-also"></a>请参阅


[**亮度**](brightness.md)

[**ColorProcessing**](colorprocessing.md)

[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[**Contrast**](contrast.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**DocumentParameters**](documentparameters.md)

[**文档**](documents.md)

[**风险**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**Format**](format.md)

[**Height**](height.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**InputSize**](inputsize.md)

[**InputSource**](inputsource.md)

[**MediaSides**](mediasides.md)

[**旋转**](rotation.md)

[**缩放**](scaling.md)

[**ScalingHeight**](scalingheight.md)

[**ScalingWidth**](scalingwidth.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

[**ScanTicket**](scanticket.md)

[**Sharpness**](sharpness.md)

[**Width**](width.md)

 

 






