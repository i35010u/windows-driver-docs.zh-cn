---
title: JobStatusEvent 元素
description: 必需的 JobStatusEvent 元素通知客户端作业的状态已更改。
ms.assetid: 8cb510ef-9622-48d0-859d-e52c9b5b8190
keywords:
- JobStatusEvent 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobStatusEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33ffd91141af72f57158b1a6181706369d28299e
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652981"
---
# <a name="jobstatusevent-element"></a>JobStatusEvent 元素


必需的**JobStatusEvent**元素通知客户端作业的状态已更改。

<a name="usage"></a>Usage
-----

```xml
<wscn:JobStatusEvent>
  child elements
</wscn:JobStatusEvent>
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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

当作业的状态发生更改时，WSD 扫描服务会向客户端发送一个**JobStatusEvent**元素。 **JobStatusEvent**包含一个[**JobStatus**](jobstatus.md)元素，该元素定义有关作业当前状态的所有信息。 第一条**JobStatusEvent**消息通常包含[**JobId**](jobid.md)元素， [**JobState**](jobstate.md)为 "**已启动**"。

<a name="examples"></a>示例
--------

下面的代码示例演示扫描设备如何向客户端通知作业253的当前状态。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/JobStatusEvent
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:JobStatusEvent>
      <wscn:JobStatus>
        <wscn:JobId>253</wscn:JobId>
        <wscn:JobState>Processing</wscn:JobState>
        <wscn:JobStateReasons>
          <wscn:JobStateReason>JobScanning</wscn:JobStateReason>
        </wscn:JobStateReasons>
        <wscn:ScansCompleted>4</wscn:ScansCompleted>
        <wscn:JobCreatedTime>2006-01-24T11:34:35.8345Z</wscn:JobCreatedTime>
      </wscn:JobStatus>
    </wscn:JobStatusEvent>
  </soap:Body
</soap:Envelope>
```

## <a name="see-also"></a>另请参阅


[**JobId**](jobid.md)

[**JobState**](jobstate.md)

[**JobStatus**](jobstatus.md)










