---
title: JobEndStateEvent 元素
description: 所需的 JobEndStateEvent 元素告知客户端扫描程序已完成处理作业。
ms.assetid: 2d5307fb-9c64-413d-8c5c-439012a44a19
keywords:
- JobEndStateEvent 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobEndStateEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a0d74c1976d7dba8bbfbce13b4970a91f2ce309
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377582"
---
# <a name="jobendstateevent-element"></a>JobEndStateEvent 元素


所需**JobEndStateEvent**元素告知客户端扫描程序已完成处理作业。

<a name="usage"></a>用法
-----

```xml
<wscn:JobEndStateEvent>
  child elements
</wscn:JobEndStateEvent>
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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务发送**JobEndStateEvent**事件元素到客户端时，扫描程序已完成作业的处理。 **JobEndStateEvent**包含标识的已完成的作业和有关其完成的详细信息的数据元素。

<a name="examples"></a>示例
--------

下面的代码示例显示了最终状态的客户端和状态的作业 253 扫描设备的通知方式。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/JobEndStateEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:JobEndStateEvent>
      <wscn:JobEndState>
        <wscn:JobId>253</wscn:JobId>
        <wscn:JobCompletedState>Completed</wscn:JobCompletedState>
        <wscn:JobCompletedStateReasons>
          <wscn:JobStateReason>JobCompletedWithWarnings</wscn:JobStateReason>
        </wscn:JobCompletedStateReasons>
        <wscn:JobName>Scan from Imaging App</wscn:JobName>
        <wscn:JobOriginatingUserName>User</wscn:JobOriginatingUserName>
        <wscn:ScansCompleted>7</wscn:ScansCompleted>
        <wscn:JobCompletedTime>2006-01-24T11:37:05.673Z</wscn:JobCompletedTime>
      </wscn:JobEndState>
    </wscn:JobEndStateEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

 

 






