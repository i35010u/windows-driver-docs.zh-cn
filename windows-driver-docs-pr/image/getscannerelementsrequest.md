---
title: GetScannerElementsRequest 元素
description: 所需的 GetScannerElementsRequest 元素使客户端请求有关扫描程序的信息。
ms.assetid: 9b5baed9-0950-4fbd-9e5b-4ad58dedb87e
keywords:
- GetScannerElementsRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn GetScannerElementsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c6865d6dde3f9981cced1e2e3b9a466010636d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330277"
---
# <a name="getscannerelementsrequest-element"></a>GetScannerElementsRequest 元素


所需**GetScannerElementsRequest**元素启用的客户端的请求，扫描程序的相关信息。

<a name="usage"></a>用法
-----

```xml
<wscn:GetScannerElementsRequest>
  child elements
</wscn:GetScannerElementsRequest>
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
<td><p><a href="requestedelements.md" data-raw-source="[&lt;strong&gt;RequestedElements&lt;/strong&gt;](requestedelements.md)"><strong>RequestedElements</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**GetScannerElementsRequest**操作。

客户端可以调用**GetScannerElementsRequest**发现的扫描服务的架构的标准和供应商扩展元素。 可供客户端的信息包括设备根级别可访问的扫描程序数据的任何部分。 此信息包括说明、 配置、 状态、 默认扫描票证和扫描服务的任何供应商扩展。

如果扫描服务成功处理了**GetScannerElementsRequest**，它将返回[ **GetScannerElementsResponse** ](getscannerelementsresponse.md)操作请求的信息。 否则，扫描服务应返回相应的错误代码。

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

<a name="examples"></a>示例
--------

在下面的代码示例中，客户端指定单个 QName 值 (wscn:ScannerDescription) 来查询有关扫描程序的说明。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsRequest>
      <wscn:RequestedElements>
        <wscn:Name>wscn:ScannerDescription</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetScannerElementsRequest>
  </soap:Body>
</soap:Envelope>
```

下面的代码示例显示了客户端的请求的扫描程序的状态。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsRequest>
      <wscn:RequestedElements>
        <wscn:Name>wscn:ScannerStatus</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetScannerElementsRequest>
  </soap:Body>
</soap:Envelope>
```

在下面的代码示例中，客户端指定两个 QName 值。 第一个 QName 是 wscn:ScannerConfiguration，并且第二个 QName 无效。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  xmlns:ihv="http://www.example.com/extension"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetScannerElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetScannerElementsRequest>
      <wscn:RequestedElements>
        <wscn:Name>wscn:ScannerConfiguration</wscn:Name>
        <wscn:Name>ihv:InvalidRequestEntry</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetScannerElementsRequest>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**GetScannerElementsResponse**](getscannerelementsresponse.md)

[**RequestedElements**](requestedelements.md)

 

 






