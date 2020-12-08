---
title: GetJobHistoryRequest 元素
description: 必需的 GetJobHistoryRequest 元素为先前完成的作业请求与作业相关的变量的摘要。
keywords:
- GetJobHistoryRequest 元素图像设备
topic_type:
- apiref
api_name:
- wscn GetJobHistoryRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67b306360edf0fb4eae13905d8020138ca06eb56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808805"
---
# <a name="getjobhistoryrequest-element"></a>GetJobHistoryRequest 元素


必需的 **GetJobHistoryRequest** 元素为先前完成的作业请求与作业相关的变量的摘要。

<a name="usage"></a>使用情况
-----

```xml
<wscn:GetJobHistoryRequest/>
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

WSD 扫描服务必须支持 **GetJobHistoryRequest** 操作元素。

客户端可以调用 **GetJobHistoryRequest** 来检索列表，其中包含之前完成的作业的与作业相关的变量的摘要。 WSD 扫描服务必须使用包含客户端请求的信息的 [**GetJobHistoryResponse**](getjobhistoryresponse.md) 操作元素或适当的错误代码进行响应。

WSD 扫描服务所保留的作业历史记录量是特定于实现的。

此操作可以返回所有常见的 [**WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何报告错误的详细信息，请参阅 [WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

<a name="examples"></a>示例
--------

下面的代码示例包含对作业历史记录的请求。

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
      https://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryRequest />
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>请参阅


[**GetJobHistoryResponse**](getjobhistoryresponse.md)

 

 






