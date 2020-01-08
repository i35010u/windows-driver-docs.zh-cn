---
title: JobEndStateEvent 元素
description: 必需的 JobEndStateEvent 元素将通知客户端扫描程序已完成处理作业。
ms.assetid: 2d5307fb-9c64-413d-8c5c-439012a44a19
keywords:
- JobEndStateEvent 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobEndStateEvent
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74bb42fa3d5533b0a99909eefaf767080d82ad83
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652983"
---
# <a name="jobendstateevent-element"></a>JobEndStateEvent 元素


必需的**JobEndStateEvent**元素将通知客户端扫描程序已完成处理作业。

<a name="usage"></a>Usage
-----

```xml
<wscn:JobEndStateEvent>
  child elements
</wscn:JobEndStateEvent>
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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

当扫描程序完成作业处理时，WSD 扫描服务会将**JobEndStateEvent**事件元素发送到客户端。 **JobEndStateEvent**包含的数据元素用于标识完成的作业及其完成的详细信息。

<a name="examples"></a>示例
--------

下面的代码示例演示扫描设备如何向客户端通知作业253的最终状态和状态。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/JobEndStateEvent
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

## <a name="see-also"></a>另请参阅


[**JobEndState**](jobendstate.md)

 

 






