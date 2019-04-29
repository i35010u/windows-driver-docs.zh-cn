---
title: GetJobElementsRequest element
description: 所需的 GetJobElementsRequest 元素请求的作业的作业 Id 元素标识与相关的信息。
ms.assetid: ba8260f4-300f-447e-ad62-d2e4fa2811ef
keywords:
- GetJobElementsRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn GetJobElementsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17c3eb4f27339aeca645f764327371b11d9875b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384558"
---
# <a name="getjobelementsrequest-element"></a>GetJobElementsRequest element


所需**GetJobElementsRequest**元素请求与作业相关的信息的[ **JobId** ](jobid.md)元素标识。

<a name="usage"></a>用法
-----

```xml
<wscn:GetJobElementsRequest>
  child elements
</wscn:GetJobElementsRequest>
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
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="requestedelements.md" data-raw-source="[&lt;strong&gt;RequestedElements&lt;/strong&gt;](requestedelements.md)"><strong>RequestedElements</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**GetJobElementsRequest**操作。

客户端可以调用**GetJobElementsRequest**来确定作业与作业相关的元素的值的[ **JobId** ](jobid.md)标识。 WSD 扫描服务必须响应**GetJobElementsResponse**。 扫描服务返回的信息必须完全符合架构的扫描作业相关部分。

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

**GetJobElementsRequest**可能也会返回以下错误。

-   **ClientErrorJobIdNotFound**

    扫描程序找不到 JobId 值相匹配的作业或作业 Id 值不在定义的范围内。

    | Fault 属性 | 定义                         |
    |----------------|------------------------------------|
    | \[Code\]       | soap:Sender                        |
    | \[Subcode\]    | wscn:ClientErrorJobIdNotFound      |
    | \[Reason\]     | 找不到指定的 JobId。 |
    | \[详细信息\]     | JobId:不正确的作业 Id             |

     

<a name="examples"></a>示例
--------

下面的代码示例请求 Fault 属性 1 标识扫描作业的状态。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="http://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="http://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='http://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobElements>
      <wscn:JobId>1</wscn:JobId>
      <wscn:RequestedElements>
        <wscn:Name>JobStatus</wscn:Name>
      </wscn:RequestedElements>
    </wscn:GetJobElements>
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**GetJobElementsResponse**](getjobelementsresponse.md)

[**JobId**](jobid.md)

[**RequestedElements**](requestedelements.md)

 

 






