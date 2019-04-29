---
title: GetActiveJobsRequest element
description: 所需的 GetActiveJobsRequest 元素请求中扫描设备的所有当前处于活动状态的作业的摘要。
ms.assetid: 4dc7bc64-b62f-4634-8f0e-64039b9f8609
keywords:
- GetActiveJobsRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn GetActiveJobsRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34af8b8822b279e7e3b31e1f2b2685b17dd0b266
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357535"
---
# <a name="getactivejobsrequest-element"></a>GetActiveJobsRequest element


所需**GetActiveJobsRequest**元素请求中扫描设备的所有当前处于活动状态的作业的摘要。

<a name="usage"></a>用法
-----

```xml
<wscn:GetActiveJobsRequest/>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


没有子元素。

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**GetActiveJobsRequest**操作。

在客户端调用**GetActiveJobsRequest**检索一个列表，其中包含所有当前处于活动状态的扫描作业与作业相关的变量的摘要。 WSD 扫描服务必须响应[ **GetActiveJobsResponse** ](getactivejobsresponse.md)元素，其中包含客户端要求的信息或相应的错误代码。

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

<a name="examples"></a>示例
--------

下面的代码示例显示了有关所有活动的扫描作业请求。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetActiveJobs
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

 

 






