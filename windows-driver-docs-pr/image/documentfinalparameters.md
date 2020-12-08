---
title: DocumentFinalParameters 元素
description: 必需的 DocumentFinalParameters 元素包含扫描设备用于获取图像的实际 DocumentParameters 元素。
keywords:
- DocumentFinalParameters 元素图像设备
topic_type:
- apiref
api_name:
- wscn DocumentFinalParameters
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 357705ea7f13762a5abd9c38f3d50a2284b0af47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832673"
---
# <a name="documentfinalparameters-element"></a>DocumentFinalParameters 元素


必需的 **DocumentFinalParameters** 元素包含扫描设备用于获取图像的实际 [**DocumentParameters**](documentparameters.md) 元素。

<a name="usage"></a>使用情况
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
<td><p><a href="exposure.md" data-raw-source="[&lt;strong&gt;Exposure&lt;/strong&gt;](exposure.md)"><strong>隐患</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="filmscanmode.md" data-raw-source="[&lt;strong&gt;FilmScanMode&lt;/strong&gt;](filmscanmode.md)"><strong>FilmScanMode</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="format.md" data-raw-source="[&lt;strong&gt;Format&lt;/strong&gt;](format.md)"><strong>形式</strong></a></p></td>
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

**DocumentFinalParameters** 元素包含的元素包含 WSD 扫描服务使用的实际扫描作业值。 由于各种原因，这些值可能不同于在作业 [**ScanTicket**](scanticket.md) 中请求的值。 每个参数都在此层次结构中表示，在已知值时必须填写。

**DocumentFinalParameters** 层次结构中的某些元素可以包含 **Override** 和 **UsedDefault** 布尔属性。 如果 **重写** 属性在元素中存在且为 true，则扫描设备使用指定值 u.i 请求的值。 如果 **UsedDefault** 属性在元素中存在且为 true，则扫描设备使用指定的默认值。

[**亮度**](brightness.md)[**ColorProcessing**](colorprocessing.md)[**CompressionQualityFactor**](compressionqualityfactor.md)[**ContentType**](contenttype.md)[**对比度**](contrast.md)[**FilmScanMode**](filmscanmode.md)[**格式**](format.md)[**高度**](height.md)[**ImagesToTransfer**](imagestotransfer.md)[**InputSource**](inputsource.md)[**旋转**](rotation.md)[**ScalingHeight**](scalingheight.md)[**ScalingWidth**](scalingwidth.md)[**ScanRegionHeight ScanRegionWidth ScanRegionXOffset**](scanregionheight.md)[**ScanRegionYOffset**](scanregionwidth.md)[**ScanRegionXOffset**](scanregionxoffset.md)[**ScanRegionYOffset**](scanregionyoffset.md)[**清晰度**](sharpness.md)[**宽度**](width.md)

以下元素可以具有 **Override** 和 **UsedDefault** 属性： [**亮度**](brightness.md)、 [**ColorProcessing**](colorprocessing.md)、 [**CompressionQualityFactor**](compressionqualityfactor.md)、 [**ContentType**](contenttype.md)、 [**对比度**](contrast.md)、 [**FilmScanMode**](filmscanmode.md)、 [**格式**](format.md)、 [**高度**](height.md)、 [**ImagesToTransfer**](imagestotransfer.md)、 [**InputSource**](inputsource.md)、 [**旋转**](rotation.md)、 [**ScalingHeight**](scalingheight.md)、 [**ScalingWidth**](scalingwidth.md)、 [**ScanRegionHeight**](scanregionheight.md)、 [**ScanRegionWidth**](scanregionwidth.md)、 [**ScanRegionXOffset**](scanregionxoffset.md)、 [**ScanRegionYOffset**](scanregionyoffset.md)、 [**清晰度**](sharpness.md)和 [**宽度**](width.md)。

## <a name="see-also"></a>请参阅


[**亮度**](brightness.md)

[**ColorProcessing**](colorprocessing.md)

[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[**对比度**](contrast.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**DocumentParameters**](documentparameters.md)

[**文档**](documents.md)

[**隐患**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**形式**](format.md)

[**高度**](height.md)

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

[**宽度**](width.md)

 

 






