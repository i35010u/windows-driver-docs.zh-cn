---
title: ScanAvailableEvent 元素
description: 必需的 ScanAvailableEvent 元素通知客户端，客户端所订阅的扫描设备已准备好扫描作业。
ms.assetid: 82ebfa36-60df-44dd-a928-e751deeea5b0
keywords:
- ScanAvailableEvent 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScanAvailableEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01802172f27f6d614954004f5e26b37a9079f05
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652947"
---
# <a name="scanavailableevent-element"></a>ScanAvailableEvent 元素


必需的**ScanAvailableEvent**元素通知客户端，客户端所订阅的扫描设备已准备好扫描作业。

<a name="usage"></a>Usage
-----

```xml
<wscn:ScanAvailableEvent>
  child elements
</wscn:ScanAvailableEvent>
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

当用户选择了扫描目标并在扫描设备上启动扫描时，WSD 扫描服务会将**ScanAvailableEvent**元素发送到已注册的客户端。

客户端必须使用 WSD 扫描服务创建订阅才能接收**ScanAvailableEvent**事件。 客户端通过 **&lt;wse：订阅&gt;** 请求操作元素向扫描服务发送请求消息，从而创建一个订阅。

订阅请求在[**ScanDestinations**](scandestinations.md) extension 元素中包含一个或多个目标。 每次发送**ScanAvailableEvent**通知时，扫描服务都将使用这些目标向下筛选到单个客户端。 此筛选器可防止扫描服务在用户按下 "扫描" 按钮时通知每个客户端。 扩展元素是在 WSD 扫描服务命名空间中定义的，然后添加到 **&lt;wse：订阅&gt;** 请求正文中。

如果 WSD 扫描服务接受客户端的请求来创建订阅，服务必须使用响应 **&lt;wse:SubscribeResponse&gt;** 响应操作元素。 订阅响应包含中的一个或多个目标响应 [**DestinationResponses**](destinationresponses.md) 扩展元素，可帮助连接到接受它扫描设备的订阅。

**&lt;Wse： 订阅&gt;** 并 **&lt;wse:SubscribeResponse&gt;** 在规范中描述的元素。

<a name="examples"></a>示例
--------

下面的代码示例演示客户端如何订阅以接收来自 WSD 扫描服务的 ScanAvailableEvent 事件。

```xml
<soap:Envelope
    xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan>
    soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
      <wsa:Action>
         https://schemas.xmlsoap.org/ws/2004/08/eventing/Subscribe
      </wsa:Action>
      <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
      <wsa:ReplyTo>
        <wsa:Address>https://www.example.com/MyEventSink</wsa:Address>
      </wsa:ReplyTo>
  </soap:Header>
  <soap:Body>
    <wse:Subscribe>
      <wse:Delivery>
        <wse:NotifyTo>
          <wsa:Address>
            https://www.example.com/MyEventSink/OnScanAvailableForMe
          </wsa:Address>
        </wse:NotifyTo>
      </wse:Delivery>
      <wse:Expires>P0Y0M0DT30H0M0S</wse:Expires>
      <wse:Filter xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan">
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

下面的代码示例显示了 WSD 扫描服务对客户端订阅请求的响应。

```xml
<soap:Envelope
    xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
    xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan">
    soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >
  <soap:Header>
    <wsa:To>https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      https://schemas.xmlsoap.org/ws/2004/08/eventing/SubscribeResponse
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

下面的代码示例演示了 WSD 扫描服务如何向客户端发送 ScanAvailableEvent。

```xml
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
  xmlns:wse="https://schemas.xmlsoap.org/ws/2004/08/eventing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding'>

  <soap:Header>
    <wsa:To>AddressofEventSink</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/ScanAvailableEvent
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

## <a name="see-also"></a>另请参阅


[**ClientContext**](clientcontext.md)

[**DestinationResponses**](destinationresponses.md)

[**ScanDestinations**](scandestinations.md)

[**ScanIdentifier**](scanidentifier.md)

 

 






