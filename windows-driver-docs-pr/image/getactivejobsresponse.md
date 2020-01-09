---
title: GetActiveJobsResponse 元素
description: 必需的 GetActiveJobsResponse 元素返回所有当前活动扫描作业的与作业相关的变量的摘要。
ms.assetid: 77efef7f-451d-49f8-80c1-6ab12c98ee7b
keywords:
- GetActiveJobsResponse 元素图像设备
topic_type:
- apiref
api_name:
- wscn GetActiveJobsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02e604cc11af151776ea059e2102abc8c0439d1d
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652977"
---
# <a name="getactivejobsresponse-element"></a>GetActiveJobsResponse 元素


必需的**GetActiveJobsResponse**元素返回所有当前活动扫描作业的与作业相关的变量的摘要。

<a name="usage"></a>Usage
-----

```xml
<wscn:GetActiveJobsResponse>
  child elements
</wscn:GetActiveJobsResponse>
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
<td><p><a href="activejobs.md" data-raw-source="[&lt;strong&gt;ActiveJobs&lt;/strong&gt;](activejobs.md)"><strong>ActiveJobs</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**GetActiveJobsResponse**操作。

客户端可以调用[**GetActiveJobsRequest**](getactivejobsrequest.md)来确定所有当前活动扫描作业的与作业相关的变量的值。 WSD 扫描服务必须使用包含客户端请求的信息的**GetActiveJobsResponse**元素或适当的错误代码进行响应。

**GetActiveJobsResponse**包含一个[**ActiveJobs**](activejobs.md)元素，该元素包含所有作业的摘要。

<a name="examples"></a>示例
--------

下面的代码示例演示如何返回没有活动扫描作业的事实。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetActiveJobsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetActiveJobsResponse>
      <wscn:ActiveJobs/>
    </wscn:GetActiveJobsResponse >
  </soap:Body>
</soap:Envelope>
```

下面的代码示例报告了两个活动扫描作业。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>
      https://schemas.xmlsoap.org/ws/2003/03/addressing/role/anonymous
    </wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetActiveJobsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetActiveJobsResponse>
      <wscn:ActiveJobs>
        <wscn:JobSummary>
          <wscn:JobId>1</wscn:JobId>
          <wscn:JobName>SampleJob 1</wscn:JobName>
          <wscn:JobOriginatingUserName>Joe.Smith</wscn:JobOriginatingUserName>
          <wscn:JobState>Processing</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>JobScanning</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>2</wscn:ScansCompleted>
        </wscn:JobSummary>
        <wscn:JobSummary>
          <wscn:JobId>2</wscn:JobId>
          <wscn:JobName>Sample Job 2</wscn:JobName>
          <wscn:JobOriginatingUserName>JaneSmith</wscn:JobOriginatingUserName>
          <wscn:JobState>Pending</wscn:JobState>
          <wscn:JobStateReasons>
            <wscn:JobStateReason>None</wscn:JobStateReason>
          </wscn:JobStateReasons>
          <wscn:ScansCompleted>0</wscn:ScansCompleted>
        </wscn:JobSummary>
      </wscn:ActiveJobs>
    </wscn:GetActiveJobsResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>另请参阅


[**ActiveJobs**](activejobs.md)

[**GetActiveJobsRequest**](getactivejobsrequest.md)










