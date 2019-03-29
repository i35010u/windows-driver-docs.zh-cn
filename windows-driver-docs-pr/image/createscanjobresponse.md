---
title: CreateScanJobResponse 元素
description: 必需的 CreateScanJobResponse 元素包含对客户端的扫描请求的 WSD 扫描服务的响应。
ms.assetid: a832bdc2-9c47-41da-ac78-a844b8f84ec1
keywords:
- CreateScanJobResponse 元素成像设备
topic_type:
- apiref
api_name:
- wscn CreateScanJobResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd61b561afd387dc7cf0c9a6d16d01996a15beb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564348"
---
# <a name="createscanjobresponse-element"></a>CreateScanJobResponse 元素


所需**CreateScanJobResponse**元素包含对客户端的扫描请求的 WSD 扫描服务的响应。

<a name="usage"></a>用法
-----

```xml
<wscn:CreateScanJobResponse>
  child elements
</wscn:CreateScanJobResponse>
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

WSD 扫描服务发送**CreateScanJobResponse**到客户端的响应中的客户端的操作元素[ **CreateScanJobRequest**](createscanjobrequest.md)。

如果客户端进行有效的扫描请求，WSD 扫描服务必须返回以下信息：

-   一个唯一[ **JobId** ](jobid.md)来标识作业。 扫描程序将生成**JobId**的方式实现定义中定义的范围。 扫描服务不重复使用，以便客户端将具有较早的作业的作业不混淆最近分配的值。
-   JobToken 中的唯一标识符。 与作业 Id 来唯一地表示扫描作业配对 JobToken。 JobToken 传递给扫描中的服务 RetrieveImageRequest 操作元素以启用扫描设备，若要验证扫描请求者实际创建扫描作业。
-   ImageInformation，其中包含有关从与当前正在验证 ScanTicket 进行扫描生成的图像数据的信息。
-   DocumentFinalParameters，其中包含此扫描作业的扫描服务使用的实际 DocumentParameters 元素。

客户端必须检索实际的图像数据从扫描服务发送一个或多个[ **RetrieveImageRequest** ](retrieveimagerequest.md)操作元素。 客户端有 60 秒发送**RetrieveImageRequest**扫描服务已答复了客户端的操作元素[ **CreateScanJobRequest**](createscanjobrequest.md)。 如果扫描服务不会收到**RetrieveImageRequest**在此时间内，它应中止与作业[ **JobStateReason** ](jobstatereason.md)的**JobTimedOut**. 如果作业包含多个文档，此超时适用之间每个连续**RetrieveImageRequest/响应**操作。

<a name="examples"></a>示例
--------

下面的代码示例说明了对 CreateScanJobRequest 的 WSD 扫描服务响应。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/CreateScanJob
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

## <a name="see-also"></a>请参阅


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DocumentFinalParameters**](documentfinalparameters.md)

[**ImageInformation**](imageinformation.md)

[**JobId**](jobid.md)

[**JobStateReason**](jobstatereason.md)

[**JobToken**](jobtoken.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 






