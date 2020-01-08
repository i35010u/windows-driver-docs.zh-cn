---
title: GetJobElementsRequest 元素
description: 必需的 GetJobElementsRequest 元素请求与 JobId 元素标识的作业相关的信息。
ms.assetid: ba8260f4-300f-447e-ad62-d2e4fa2811ef
keywords:
- GetJobElementsRequest 元素图像设备
topic_type:
- apiref
api_name:
- wscn GetJobElementsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e4f663869f2da91fcfe46d0bba0c1f42854eb9
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652995"
---
# <a name="getjobelementsrequest-element"></a>GetJobElementsRequest 元素


必需的**GetJobElementsRequest**元素请求与[**JobId**](jobid.md)元素标识的作业相关的信息。

<a name="usage"></a>Usage
-----

```xml
<wscn:GetJobElementsRequest>
  child elements
</wscn:GetJobElementsRequest>
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

客户端可以调用**GetJobElementsRequest**来确定[**JobId**](jobid.md)标识的作业相关元素的值。 WSD 扫描服务必须使用**GetJobElementsResponse**进行响应。 扫描服务返回的信息必须完全符合与扫描作业相关的架构部分。

此操作可以返回所有常见的[**WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

**GetJobElementsRequest**可能还会返回以下错误。

-   **ClientErrorJobIdNotFound**

    扫描仪找不到与 JobId 值匹配的作业，或 JobId 值不在定义的范围内。

    | 错误属性 | 定义                         |
    |----------------|------------------------------------|
    | 代码\[\]       | soap：发送方                        |
    | \[子代码\]    | wscn:ClientErrorJobIdNotFound      |
    | \[原因\]     | 找不到指定的 JobId。 |
    | \[详细信息\]     | JobId： JobId 不正确             |

     

<a name="examples"></a>示例
--------

下面的代码示例请求错误属性1标识的扫描作业的状态。

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
  xmlns:wsa="https://schemas.xmlsoap.org/ws/2003/03/addressing"
  xmlns:wscn="https://schemas.microsoft.com/windows/2006/01/wdp/scan"
  soap:encodingStyle='https://www.w3.org/2002/12/soap-encoding' >

  <soap:Header>
    <wsa:To>AddressofScannerService</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobElements
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

## <a name="see-also"></a>另请参阅


[**GetJobElementsResponse**](getjobelementsresponse.md)

[**JobId**](jobid.md)

[**RequestedElements**](requestedelements.md)

 

 






