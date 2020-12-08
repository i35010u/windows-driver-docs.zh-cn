---
title: DocumentParameters 元素
description: 可选的 DocumentParameters 元素指定要应用于作业中的文档的图像处理函数。
keywords:
- DocumentParameters 元素图像设备
topic_type:
- apiref
api_name:
- wscn DocumentParameters
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02f4ab945bf66a80da41307cd247395fa5ea1be6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789897"
---
# <a name="documentparameters-element"></a>DocumentParameters 元素


可选的 **DocumentParameters** 元素指定要应用于作业中的文档的图像处理函数。

<a name="usage"></a>使用情况
-----

```xml
<wscn:DocumentParameters>
  child elements
</wscn:DocumentParameters>
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
<td><p><a href="defaultscanticket.md" data-raw-source="[&lt;strong&gt;DefaultScanTicket&lt;/strong&gt;](defaultscanticket.md)"><strong>DefaultScanTicket</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**DocumentParameters** 元素指定将应用于作业或文档的图像处理函数及其值。

在 [**CreateScanJobRequest**](createscanjobrequest.md)操作过程中，客户端可以选择在 **ScanTicket** 元素内提供文档处理参数。 WSD 扫描服务必须验证客户端提供的所有数据，以确保将每个子元素设置为在 [**ScannerConfiguration**](scannerconfiguration.md) 元素中指定的有效值。

如果客户端不提供任何，则 WSD 扫描 Servie 应使用其默认 **DocumentParameters** 值。

## <a name="see-also"></a>请参阅


[**CompressionQualityFactor**](compressionqualityfactor.md)

[**ContentType**](contenttype.md)

[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**隐患**](exposure.md)

[**FilmScanMode**](filmscanmode.md)

[**形式**](format.md)

[**ImagesToTransfer**](imagestotransfer.md)

[**InputSize**](inputsize.md)

[**InputSource**](inputsource.md)

[**MediaSides**](mediasides.md)

[**旋转**](rotation.md)

[**缩放**](scaling.md)

[**ScanTicket**](scanticket.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






