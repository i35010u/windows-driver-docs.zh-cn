---
title: CreateScanJobResponse 元素
description: 必需的 CreateScanJobResponse 元素包含 WSD 扫描服务对客户端扫描请求的响应。
ms.assetid: a832bdc2-9c47-41da-ac78-a844b8f84ec1
keywords:
- CreateScanJobResponse 元素图像设备
topic_type:
- apiref
api_name:
- wscn CreateScanJobResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa2db14d95976c4f47c68b53cf5f60ea6593648
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652985"
---
# <a name="createscanjobresponse-element"></a>CreateScanJobResponse 元素


必需的**CreateScanJobResponse**元素包含 WSD 扫描服务对客户端扫描请求的响应。

<a name="usage"></a>Usage
-----

```xml
<wscn:CreateScanJobResponse>
  child elements
</wscn:CreateScanJobResponse>
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
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="imageinformation.md" data-raw-source="[&lt;strong&gt;ImageInformation&lt;/strong&gt;](imageinformation.md)"><strong>ImageInformation</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobtoken.md" data-raw-source="[&lt;strong&gt;JobToken&lt;/strong&gt;](jobtoken.md)"><strong>JobToken</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**CreateScanJobResponse**操作元素。

WSD 扫描服务会向客户端发送**CreateScanJobResponse**操作元素，以响应客户端的[**CreateScanJobRequest**](createscanjobrequest.md)。

如果客户端发出了有效的扫描请求，则 WSD 扫描服务必须返回以下信息：

-   用于标识作业的唯一[**JobId**](jobid.md) 。 扫描程序在定义的范围内以实现定义的方式生成**JobId** 。 扫描服务不能重复使用最近分配的值，因此客户端不会将作业与较旧的作业混淆。
-   JobToken 中的唯一标识符。 JobToken 与 JobId 配对，以唯一表示扫描作业。 JobToken 传递给 RetrieveImageRequest 操作元素中的扫描服务，以使扫描设备能够验证扫描请求者是否确实创建了扫描作业。
-   ImageInformation，其中包含与当前正在验证的 ScanTicket 进行的扫描有关得到的图像数据有关的信息。
-   DocumentFinalParameters，其中包含扫描服务用于此扫描作业的实际 DocumentParameters 元素。

客户端必须通过发送一个或多个[**RetrieveImageRequest**](retrieveimagerequest.md)操作元素，从扫描服务检索实际图像数据。 在扫描服务响应客户端的[**CreateScanJobRequest**](createscanjobrequest.md)之后，客户端有60秒的时间来发送**RetrieveImageRequest**操作元素。 如果扫描服务在这段时间内没有收到**RetrieveImageRequest** ，它应中止[**JobStateReason**](jobstatereason.md)为**JobTimedOut**的作业。 如果作业包含多个文档，则此超时适用于每个连续的**RetrieveImageRequest/响应**操作。

<a name="examples"></a>示例
--------

下面的代码示例演示对 CreateScanJobRequest 的 WSD 扫描服务响应。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheCreateScanJobRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:CreateScanJobResponse>
      <wscn:JobId>1</wscn:JobId>
      <wscn:JobToken>Job9876TokenString</wscn:JobToken>
      <wscn:ImageInformation>
        <wscn:MediaFrontImageInfo>
          <wscn:PixelsPerLine>900</wscn:PixelsPerLine>
          <wscn:NumberOfLines>1500</wscn:NumberOfLines>
          <wscn:BytesPerLine>113</wscn:BytesPerLine>
        </wscn:MediaFrontImageInfo>
      </wscn:ImageInformation>
      <wscn:DocumentFinalParamters>
        <wscn:Format>jfif</wscn:Format>
        <wscn:CompressionQualityFactor>45</wscn:CompressionQualityFactor>
        <wscn:ImagesToTransfer>0</wscn:ImagesToTransfer>
        <wscn:InputSource>Platen</wscn:InputSource>
        <wscn:ContentType>Auto</wscn:ContentType>
        <wscn:InputSize>
          <wscn:InputMediaSize>
            <wscn:Width wscn:Override="true">8500</wscn:Width>
            <wscn:Height wscn:Override="true">11000</wscn:Height>
          </wscn:InputMediaSize>
        </wscn:InputSize>
        <wscn:Exposure>
          <wscn:ExposureSettings>
            <wscn:Contrast wscn:UsedDefault="true">0</wscn:Contrast>
            <wscn:Brightness wscn:UsedDefault="true">0</wscn:Brightness>
            <wscn:Sharpness wscn:UsedDefault="true">0</wscn:Sharpness>
          </wscn:ExposureSettings>
        </wscn:Exposure>
        <wscn:Scaling>
          <wscn:ScalingWidth>125</wscn:ScalingWidth>
          <wscn:ScalingHeight>125</wscn:ScalingHeight>
        </wscn:Scaling>
        <wscn:Rotation wscn:UsedDefault="true">0</wscn:Rotation>
        <wscn:MediaSides>
          <wscn:MediaFront>
            <wscn:ScanRegion>
              <wscn:ScanRegionXOffset wscn:UsedDefault="true">
                0
              </wscn:ScanRegionXOffset>
              <wscn:ScanRegionYOffset wscn:UsedDefault="true">
                0
              </wscn:ScanRegionYOffset>
              <wscn:ScanRegionWidth wscn:UsedDefault="true">
                8500
              </wscn:ScanRegionWidth>
              <wscn:ScanRegionHeight wscn:UsedDefault="true">
                11000
              </wscn:ScanRegionHeight>
            </wscn:ScanRegion>
            <wscn:ColorProcessing wscn:UsedDefault="true">
              RGB24
            </wscn:ColorProcessing>
            <wscn:Resolution>
              <wscn:Width>300</wscn:Width>
              <wscn:Height>300</wscn:Height>
            </wscn:Resolution>
          </wscn:MediaFront>
        </wscn:MediaSides>
      </wscn:DocumentFinalParamters>
    </wscn:CreateScanJobResponse>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>另请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**ImageInformation**](imageinformation.md)

[**JobId**](jobid.md)

[**JobStateReason**](jobstatereason.md)

[**JobToken**](jobtoken.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






