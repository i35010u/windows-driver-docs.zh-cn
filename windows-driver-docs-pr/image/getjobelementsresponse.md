---
title: GetJobElementsResponse 元素
description: 必需的 GetJobElementsResponse 元素返回客户端请求的与作业相关的信息。
ms.assetid: b27c1aba-eb5f-4446-ab34-c03a969e954f
keywords:
- GetJobElementsResponse 元素图像设备
topic_type:
- apiref
api_name:
- wscn GetJobElementsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2db1cd742c000d209ad6f82f86d389970e01d44a
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652975"
---
# <a name="getjobelementsresponse-element"></a>GetJobElementsResponse 元素


必需的**GetJobElementsResponse**元素返回客户端请求的与作业相关的信息。

<a name="usage"></a>Usage
-----

```xml
<wscn:GetJobElementsResponse>
  child elements
</wscn:GetJobElementsResponse>
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
<td><p><a href="jobelements.md" data-raw-source="[&lt;strong&gt;JobElements&lt;/strong&gt;](jobelements.md)"><strong>JobElements</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**GetJobElementsResponse**操作。

客户端调用**GetJobElementsRequest**来确定[**JobId**](jobid.md)标识的作业的与作业相关的元素的值。 WSD 扫描服务必须通过包含所需信息的**GetJobElementsResponse**元素来做出响应。 扫描服务返回的信息必须完全符合与扫描作业相关的架构部分。

<a name="examples"></a>示例
--------

在下面的代码示例中，扫描服务为 JobId 1 标识的作业返回作业状态。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetJobElementsRequest</wsa:RelatesTo>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobElementsResponse>
      <wscn:JobElements>
        <wscn:ElementData wscn:Name="JobStatus" wscn:Valid="true">
          <wscn:JobStatus>
            <wscn:JobId>1</wscn:JobId>
            <wscn:JobState>Completed</wscn:JobState>
            <wscn:JobStateReasons>
              <wscn:JobStateReason>None</wscn:JobStateReason>
            </wscn:JobStateReasons>
            <wscn:ScansCompleted>1</wscn:ScansCompleted>
          </wscn:JobStatus>
        </wscn:ElementData>
      </wscn:JobElements>
    </wscn:GetJobElementsResponse >
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>另请参阅


[**GetJobElementsRequest**](getjobelementsrequest.md)

[**JobElements**](jobelements.md)

[**JobId**](jobid.md)










