---
title: ValidateScanTicketRequest 元素
description: 所需的 ValidateScanTicketRequest 操作元素使客户端能够确定未来扫描操作的设置是否有效。
keywords:
- ValidateScanTicketRequest 元素图像设备
topic_type:
- apiref
api_name:
- wscn ValidateScanTicketRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a32416576fa7873014df79bf1ac06a2b10bd8d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819523"
---
# <a name="validatescanticketrequest-element"></a>ValidateScanTicketRequest 元素


所需的 **ValidateScanTicketRequest** 操作元素使客户端能够确定未来扫描操作的设置是否有效。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ValidateScanTicketRequest>
  child elements
</wscn:ValidateScanTicketRequest>
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
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

客户端可以使用 **ValidateScanTicketRequest** 元素来验证各种设置更改和组合。

[**ScanTicket**](scanticket.md) 包含客户端在将来的扫描操作中要提交的所有设置。 **ScanTicket** 只能包含客户端要在扫描程序中替代的处理元素，也可以包含 WSD 扫描服务支持的每个可能的元素。

如果 WSD 扫描服务成功处理 **ValidateScanTicketRequest**，它将在 [**ValidateScanTicketResponse**](validatescanticketresponse.md) 操作中返回其验证信息。 否则，扫描服务应返回相应的错误代码。

此操作可以返回所有常见的 [**WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何报告错误的详细信息，请参阅 [WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

此操作还可能会返回以下错误代码：

-   **ClientErrorConflictingRequiredParameters**

    两个或多个 DocumentParameters 元素之间存在冲突，每个元素都将 MustHonor 属性设置为 true。 使用 MustHonor set true 提供的所有设置都将导致设备冲突。 扫描服务无法解决此冲突，因此 ScanTicket 被视为无效。

    | 错误属性 | 定义                                                                                                                                                     |
    |----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[代码\]       | soap：发送方                                                                                                                                                    |
    | \[子代码\]    | wscn:ClientErrorConflictingRequiredParameters                                                                                                                  |
    | \[原因\]     | DocumentParameters 元素中的多个元素的 MustHonor 设置为 true，但将设置为 true 的所有设置都将导致扫描器设备冲突。 |
    | Detail\[\]     | 无                                                                                                                                                           |

     

<a name="examples"></a>示例
--------

下面的代码示例演示对有效扫描票证的验证请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketRequest>
      <wscn:ScanTicket>
        <wscn:JobDescription>
          <wscn:JobName>Photo Scan</wscn:JobName>
          <wscn:JobOriginatingUserName>RogerSmith</JobOriginatingUserName>
        </wscn:JobDescription>
        <wscn:DocumentParameters>
          <wscn:Format>dib</wscn:Format>
          <wscn:InputSource>Platen</wscn:InputSource>
          <wscn:ContentType>Auto</wscn:ContentType>
          <wscn:InputSize>
            <wscn:InputMediaSize>
              <wscn:Width>3000</wscn:Width>
              <wscn:Height>5000</wscn:Height>
            </wscn:InputMediaSize>
          </wscn:InputSize>
          <wscn:Scaling>
            <wscn:ScalingWidth>125</wscn:ScalingWidth>
            <wscn:ScalingHeight>125</wscn:ScalingHeight>
          </wscn:Scaling>
          <wscn:MediaSides>
            <wscn:MediaFront>
              <wscn:ColorProcessing>GrayScale4</wscn:ColorProcessing>
              <wscn:Resolution>
                <wscn:Width>300</wscn:Width>
                <wscn:Height>300</wscn:Height>
              </wscn:Resolution>
            </wscn:MediaFront>
          </wscn:MediaSides>
        </wscn:DocumentParameters>
      </wscn:ScanTicket>
    </wscn:ValidateScanTicketRequest>
  </soap:Body>
  </soap:Envelope>
```

下面的代码示例演示对无效扫描票证的验证请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ValidateScanTicketRequest>
      <wscn:ScanTicket>
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
            <wscn:ScalingWidth>1250</wscn:ScalingWidth>
            <wscn:ScalingHeight>1250</wscn:ScalingHeight>
          </wscn:Scaling>
          <wscn:MediaSides>
          <wscn:MediaFront>
          <wscn:Resolution>
            <wscn:Width>350</wscn:Width>
            <wscn:Height>350</wscn:Height>
          </wscn:Resolution>
          <wscn:MediaFront>
          <wscn:MediaSides>
        </wscn:DocumentParameters>
      </wscn:ScanTicket>
    </wscn:ValidateScanTicketRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅

[**ScanTicket**](scanticket.md)

[**ValidateScanTicketRequest**](validatescanticketrequest.md)
