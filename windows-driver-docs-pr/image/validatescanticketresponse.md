---
title: ValidateScanTicketResponse 元素
description: 所需的 ValidateScanTicketResponse 操作将通知客户端客户端提交的 ScanTicket 是否有效。
keywords:
- ValidateScanTicketResponse 元素图像设备
topic_type:
- apiref
api_name:
- wscn ValidateScanTicketResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7df514b21a69bfdbb51ef00fbd63674a394f0ee6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819515"
---
# <a name="validatescanticketresponse-element"></a>ValidateScanTicketResponse 元素


所需的 **ValidateScanTicketResponse** 操作将通知客户端客户端提交的 [**ScanTicket**](scanticket.md) 是否有效。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ValidateScanTicketResponse>
  child elements
</wscn:ValidateScanTicketResponse>
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
<td><p><a href="validationinfo.md" data-raw-source="[&lt;strong&gt;ValidationInfo&lt;/strong&gt;](validationinfo.md)"><strong>ValidationInfo</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

客户端提交要在 [**ValidateScanTicketRequest**](validatescanticketrequest.md)操作中检查的 [**ScanTicket**](scanticket.md)元素。 在成功处理 **ValidateScanTicketRequest** 后，WSD 扫描服务必须响应包含所有验证信息的 **ValidateScanTicketResponse** 元素。

<a name="examples"></a>示例
--------

下面的代码示例演示了在客户端提交有效扫描票证后对客户端的响应。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="https://www.w3.org/2003/12/xop/include"
  xmlns:xop-mime="https://www.w3.org/2003/12/xop/mime"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheValidateScanTicketRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketResponse>
      <wscn:ValidationInfo>
        <wscn:ValidTicket>true</wscn:ScanIdentifierValidTicket>
          <wscn:ImageInformation>
          <wscn:MediaFrontImageInfo>
            <wscn:PixelsPerLine>900</wscn:PixelsPerLine>
            <wscn:NumberOfLines>1500</wscn:NumberOfLines>
            <wscn:BytesPerLine>113</wscn:BytesPerLine>
          </wscn:MediaFrontImageInfo>
        </wscn:ImageInformation>
      </wscn:ValidationInfo>
    </wscn:ValidateScanTicketResponse>
  </soap:Body>
</soap:Envelope>
```

下面的代码示例演示了当客户端提交了无效的扫描票证时对客户端的响应。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:xop="https://www.w3.org/2003/12/xop/include"
  xmlns:xop-mime="https://www.w3.org/2003/12/xop/mime"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheValidateScanTicketRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketResponse>
      <wscn:ValidationInfo>
        <wscn:ValidTicket>false</wscn:ValidTicket>
        <wscn:ImageInformation>
          <wscn:MediaFrontImageInfo>
            <wscn:PixelsPerLine>0</wscn:PixelsPerLine>
            <wscn:NumberOfLines>0</wscn:NumberOfLines>
            <wscn:BytesPerLine>0</wscn:BytesPerLine>
          </wscn:MediaFrontImageInfo>
        </wscn:ImageInformation>
        <wscn:ValidScanTicket>
          <wscn:JobDescription>
            <wscn:JobName>Photo Scan</wscn:JobName>
            <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
          </wscn:JobDescription>
          <wscn:DocumentParameters>
            <wscn:Format>jfif</wscn:Format>
            <wscn:InputSource>Platen</wscn:InputSource>
            <wscn:ContentType>Auto</wscn:ContentType>
            <wscn:InputSize>
              <wscn:DocumentSizeAutoDetect>true</wscn:DocumentSizeAutoDetect>
            </wscn:InputSize>
            <wscn:Scaling>
              <wscn:ScalingWidth>1000</wscn:ScalingWidth>
              <wscn:ScalingHeight>1000</wscn:ScalingHeight>
            </wscn:Scaling>
            <wscn:MediaSides>
              <wscn:MediaFront>
                <wscn:Resolution>
                  <wscn:Width>300</wscn:Width>
                  <wscn:Height>300</wscn:Height>
                </wscn:Resolution>
              </wscn:MediaFront>
            </wscn:MediaSides>
          </wscn:DocumentParameters>
        </wscn:ValidScanTicket>
      </wscn:ValidationInfo>
    </wscn:ValidateScanTicketResponse>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅

[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)

[**ValidationInfo**](validationinfo.md)
