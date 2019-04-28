---
title: JobStatusEvent 元素
description: 所需的 JobStatusEvent 元素告知客户端作业的状态已更改。
ms.assetid: 8cb510ef-9622-48d0-859d-e52c9b5b8190
keywords:
- JobStatusEvent 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobStatusEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d24694e35bc5ce8863c62f4401a481097df495
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348765"
---
# <a name="jobstatusevent-element"></a>JobStatusEvent 元素


所需**JobStatusEvent**元素告知作业的状态已更改的客户端。

<a name="usage"></a>用法
-----

```xml
<wscn:JobStatusEvent>
  child elements
</wscn:JobStatusEvent>
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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务发送**JobStatusEvent**到客户端时作业的状态已更改的元素。 **JobStatusEvent**包含[ **JobStatus** ](jobstatus.md)元素，用于定义所有作业的当前状态有关的信息。 第一个**JobStatusEvent**消息通常将包括[ **JobId** ](jobid.md)元素和一个[ **JobState** ](jobstate.md)的**启动**。

<a name="examples"></a>示例
--------

下面的代码示例显示了扫描设备通知有关作业 253 的当前状态的客户端的方式。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/JobStatusEvent
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

## <a name="see-also"></a>请参阅


[**JobId**](jobid.md)

[**JobState**](jobstate.md)

[**JobStatus**](jobstatus.md)










