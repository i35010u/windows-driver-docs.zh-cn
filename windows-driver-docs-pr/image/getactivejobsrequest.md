---
title: GetActiveJobsRequest 元素
description: 必需的 GetActiveJobsRequest 元素请求扫描设备中所有当前处于活动状态的作业的摘要。
keywords:
- GetActiveJobsRequest 元素图像设备
topic_type:
- apiref
api_name:
- wscn GetActiveJobsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdfe668e90caca8d9c8876e2b7f546d672b616b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808227"
---
# <a name="getactivejobsrequest-element"></a>GetActiveJobsRequest 元素


必需的 **GetActiveJobsRequest** 元素请求扫描设备中所有当前处于活动状态的作业的摘要。

<a name="usage"></a>使用情况
-----

```xml
<wscn:GetActiveJobsRequest/>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


没有任何子元素。

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持 **GetActiveJobsRequest** 操作。

客户端调用 **GetActiveJobsRequest** 来检索列表，该列表包含所有当前活动扫描作业的与作业相关的变量的摘要。 WSD 扫描服务必须使用包含客户端请求的信息的 [**GetActiveJobsResponse**](getactivejobsresponse.md) 元素或适当的错误代码进行响应。

此操作可以返回所有常见的 [**WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何报告错误的详细信息，请参阅 [WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

<a name="examples"></a>示例
--------

下面的代码示例演示了对所有活动扫描作业的请求。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetActiveJobsRequest />
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**GetActiveJobsResponse**](getactivejobsresponse.md)

 

 






