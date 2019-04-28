---
title: GetJobHistoryResponse 元素
description: 所需的 GetJobHistoryResponse 元素返回的已完成的作业的摘要。
ms.assetid: 85c9edb4-fe6c-49a7-899a-71ce65e38852
keywords:
- GetJobHistoryResponse 元素成像设备
topic_type:
- apiref
api_name:
- wscn GetJobHistoryResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e04a3256ed576a77e70ca853278675f3f550791b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346197"
---
# <a name="getjobhistoryresponse-element"></a>GetJobHistoryResponse 元素


所需**GetJobHistoryResponse**元素返回的已完成的作业的摘要。

<a name="usage"></a>用法
-----

```xml
<wscn:GetJobHistoryResponse>
  child elements
</wscn:GetJobHistoryResponse>
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
<td><p><a href="jobhistory.md" data-raw-source="[&lt;strong&gt;JobHistory&lt;/strong&gt;](jobhistory.md)"><strong>JobHistory</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**GetJobHistoryResponse**操作元素。

客户端可以调用[ **GetJobHistoryRequest** ](getjobhistoryrequest.md)来确定以前已完成作业与作业相关的变量的值。 WSD 扫描服务必须响应**GetJobHistoryResponse**操作元素，其中包含客户端要求的信息或相应的错误代码。

WSD 扫描服务维护的作业历史记录量是特定于实现的。

<a name="examples"></a>示例
--------

下面的代码示例演示如何在作业历史记录的客户端的请求的响应中返回任何作业历史记录。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory />
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

下面的代码示例返回的作业和关联的数据，最后两个已完成作业的列表。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      http://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobHistoryRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryResponse>
      <wscn:JobHistory>
        <wscn:JobSummary>
          <wscn:JobId>1</wscn:JobId>
          <wscn:JobName>SampleJob 1</wscn:JobName>
          <wscn:JobOriginatingUserName>Joe.Smith</wscn:JobOriginatingUserName>
          <wscn:JobState>Completed</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>None</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>4</wscn:ScansCompleted>
        </wscn:JobSummary>
        <wscn:JobSummary>
          <wscn:JobId>2</wscn:JobId>
          <wscn:JobName>Sample Job 2</wscn:JobName>
          <wscn:JobOriginatingUserName>JaneRogers</wscn:JobOriginatingUserName>
          <wscn:JobState>Canceled</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>JobCanceledAtDevice</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>1</wscn:ScansCompleted>
        </wscn:JobSummary>
      </wscn:JobHistory>
    </wscn:GetJobHistoryResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**GetJobHistoryRequest**](getjobhistoryrequest.md)

[**JobHistory**](jobhistory.md)










