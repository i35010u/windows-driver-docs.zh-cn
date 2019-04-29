---
title: ValidateScanTicketRequest 元素
description: 所需的 ValidateScanTicketRequest 操作元素使客户端以确定将来扫描操作的设置是否有效。
ms.assetid: 366b0d71-1494-48fa-94f5-1832d7f119a4
keywords:
- ValidateScanTicketRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn ValidateScanTicketRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dda1f11b6123105b0f2c5abfce44704d3d3fd38b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356149"
---
# <a name="validatescanticketrequest-element"></a>ValidateScanTicketRequest 元素


所需**ValidateScanTicketRequest**操作元素使客户端以确定将来扫描操作的设置是否有效。

<a name="usage"></a>用法
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

可以使用客户端**ValidateScanTicketRequest**要验证各种设置的更改和组合元素。

[**ScanTicket** ](scanticket.md)包含所有客户端想要在将来扫描操作中提交的设置。 **ScanTicket**可以包含仅处理元素的客户端想要重写中扫描程序，也可以包含在 WSD 扫描服务中支持的每个可能元素。

如果已成功处理了 WSD 扫描服务**ValidateScanTicketRequest**，它将返回其验证信息中的[ **ValidateScanTicketResponse** ](validatescanticketresponse.md)操作。 否则，扫描服务应返回相应的错误代码。

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

此操作可能也会返回以下错误代码：

-   **ClientErrorConflictingRequiredParameters**

    则会发生冲突之间两个或多个 DocumentParameters 元素，每个包含 MustHonor 属性设置为 true。 使用所有随附 MustHonor 设置为 true 的设置会导致设备冲突。 扫描服务无法解决此冲突，因此 ScanTicket 被视为无效。

    | Fault 属性 | 定义                                                                                                                                                     |
    |----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | \[Code\]       | soap:Sender                                                                                                                                                    |
    | \[Subcode\]    | wscn:ClientErrorConflictingRequiredParameters                                                                                                                  |
    | \[Reason\]     | DocumentParameters 元素中的多个元素具有 MustHonor 设置为 true，但应用所有设置设置为 true 则冲突中扫描程序设备。 |
    | \[详细信息\]     | 无                                                                                                                                                           |

     

<a name="examples"></a>示例
--------

下面的代码示例显示了有效扫描票证验证请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
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

下面的代码示例显示了一个无效的扫描票证验证请求。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ValidateScanTicket
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
