---
title: ScanAvailableEvent 元素
description: 所需的 ScanAvailableEvent 元素告知客户端在客户端所订阅的扫描设备已准备好扫描作业。
ms.assetid: 82ebfa36-60df-44dd-a928-e751deeea5b0
keywords:
- ScanAvailableEvent 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScanAvailableEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2fa10ab3ecc8d0929617ca0648d89c0cd941c2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364379"
---
# <a name="scanavailableevent-element"></a>ScanAvailableEvent 元素


所需**ScanAvailableEvent**元素告知客户端在客户端所订阅的扫描设备已准备好扫描作业。

<a name="usage"></a>用法
-----

```xml
<wscn:ScanAvailableEvent>
  child elements
</wscn:ScanAvailableEvent>
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
<td><p><a href="clientcontext.md" data-raw-source="[&lt;strong&gt;ClientContext&lt;/strong&gt;](clientcontext.md)"><strong>ClientContext</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanidentifier.md" data-raw-source="[&lt;strong&gt;ScanIdentifier&lt;/strong&gt;](scanidentifier.md)"><strong>ScanIdentifier</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务发送**ScanAvailableEvent**到已注册客户端，当用户已选择了扫描目标并启动一次扫描在扫描设备的元素。

客户端必须与 WSD 扫描服务以接收创建订阅**ScanAvailableEvent**事件。 客户端通过将请求消息发送到扫描服务通过创建订阅 **&lt;wse： 订阅&gt;** 请求操作元素。

订阅请求包含的一个或多个目的地[ **ScanDestinations** ](scandestinations.md)扩展元素。 扫描服务将使用这些目标以筛选出单个客户端每次发送**ScanAvailableEvent**通知。 此筛选器可防止在用户按扫描按钮时通知每个客户端扫描服务。 扩展元素是 WSD 扫描服务命名空间中定义，然后添加到 **&lt;wse： 订阅&gt;** 请求正文。

如果 WSD 扫描服务接受客户端的请求来创建订阅，服务必须使用响应 **&lt;wse:SubscribeResponse&gt;** 响应操作元素。 订阅响应包含中的一个或多个目标响应 [**DestinationResponses**](destinationresponses.md) 扩展元素，可帮助连接到接受它扫描设备的订阅。

**&lt;Wse： 订阅&gt;** 并 **&lt;wse:SubscribeResponse&gt;** 在规范中描述的元素。

<a name="examples"></a>示例
--------

下面的代码示例演示如何在客户端订阅从 WSD 扫描服务接收 ScanAvailableEvent 事件。

```xml
<soap:Envelope
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan>
    soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
      <wsa:Action>
         http://schemas.xmlsoap.org/ws/2004/08/eventing/Subscribe
      </wsa:Action>
      <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
      <wsa:ReplyTo>
        <wsa:Address>http://www.example.com/MyEventSink</wsa:Address>
      </wsa:ReplyTo>
  </soap:Header>
  <soap:Body>
    <wse:Subscribe>
      <wse:Delivery>
        <wse:NotifyTo>
          <wsa:Address>
            http://www.example.com/MyEventSink/OnScanAvailableForMe
          </wsa:Address>
        </wse:NotifyTo>
      </wse:Delivery>
      <wse:Expires>P0Y0M0DT30H0M0S</wse:Expires>
      <wse:Filter xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan">
        ScanAvailableEvent
      </wse:Filter>
      <wscn:ScanDestinations>
        <wscn:ScanDestination>
          <wscn:ClientDisplayString>Den Computer</wscn:ClientDisplayString>
          <wscn:ClientContext>App1ScanID2345</wscn:ClientContext>
        </wscn:ScanDestination>
      </wscn:ScanDestinations>
    </wse:Subscribe>
    </soap:Body
</soap:Envelope>
```

下面的代码示例演示客户端的订阅请求的 WSD 扫描服务的响应。

```xml
<soap:Envelope
    xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan">
    soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      http://schemas.xmlsoap.org/ws/2004/08/eventing/SubscribeResponse
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheSubscribe</wsa:RelatesTo>
  </soap:Header>
  <soap:Body>
    <wse:SubscribeResponse>
        <wse:SubscriptionManager>
             <!-- Elements removed for clarity  -->
        </wse:SubscriptionManager>
        <wse:Expires>P0Y0M0DT30H0M0S</wse:Expires>
        <wscn:DestinationResponses>
          <wscn:DestinationResponse>
            <wscn:ClientContext>App1ScanID2345</wscn:ClientContext>
            <wscn:DestinationToken>Client3478</wscn:DestinationToken>
          </wscn:DestinationResponse>
        </wscn:DestinationResponses>
      </wse:SubscribeResponse>
    </soap:Body
</soap:Envelope>
```

下面的代码示例演示如何 WSD 扫描服务将 ScanAvailableEvent 发送给客户端。

```xml
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="http://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/ScanAvailableEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:ScanAvailableEvent>
      <wscn:ClientContext>App1ScanID2345</wscn:ClientContext>
      <wscn:ScanIdentifier>AnyUniqueIdentifierSuchAsAGUID</wscn:ScanIdentifier>
    </wscn:ScanAvailableEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**ClientContext**](clientcontext.md)

[**DestinationResponses**](destinationresponses.md)

[**ScanDestinations**](scandestinations.md)

[**ScanIdentifier**](scanidentifier.md)

 

 






