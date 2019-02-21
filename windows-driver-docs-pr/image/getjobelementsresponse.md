---
title: GetJobElementsResponse element
description: 所需的 GetJobElementsResponse 元素返回的客户端请求的作业相关信息。
ms.assetid: b27c1aba-eb5f-4446-ab34-c03a969e954f
keywords:
- GetJobElementsResponse 元素成像设备
topic_type:
- apiref
api_name:
- wscn GetJobElementsResponse
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f702c3e0b8182ca84ff0317de778fd02a22f0c2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521765"
---
# <a name="getjobelementsresponse-element"></a>GetJobElementsResponse element


所需**GetJobElementsResponse**元素返回的客户端请求的作业相关信息。

<a name="usage"></a>用法
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

在客户端调用**GetJobElementsRequest**来确定作业与作业相关的元素的值的[ **JobId** ](jobid.md)标识。 WSD 扫描服务必须响应**GetJobElementsResponse**元素，其中包含所需的信息。 扫描服务返回的信息必须完全符合架构的扫描作业相关部分。

<a name="examples"></a>示例
--------

在下面的代码示例中，扫描服务将返回 JobId 1 标识作业的作业状态。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
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










