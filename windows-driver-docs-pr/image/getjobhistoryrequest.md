---
title: GetJobHistoryRequest element
description: 所需的 GetJobHistoryRequest 元素请求与作业相关的变量之前已完成作业的摘要。
ms.assetid: 679a2256-2b3f-4a54-be06-8b414acab679
keywords:
- GetJobHistoryRequest 元素成像设备
topic_type:
- apiref
api_name:
- wscn GetJobHistoryRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76f49c102a7756f109d077fb517d6182712d33d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522507"
---
# <a name="getjobhistoryrequest-element"></a>GetJobHistoryRequest element


所需**GetJobHistoryRequest**元素请求与作业相关的变量之前已完成作业的摘要。

<a name="usage"></a>用法
-----

```xml
<wscn:GetJobHistoryRequest/>
```

<a name="attributes"></a>属性
----------

没有特性。

## <a name="child-elements"></a>子元素


没有子元素。

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务必须支持**GetJobHistoryRequest**操作元素。

客户端可以调用**GetJobHistoryRequest**检索一个列表，其中包含以前已完成作业与作业相关的变量的摘要。 WSD 扫描服务必须响应[ **GetJobHistoryResponse** ](getjobhistoryresponse.md)操作元素，其中包含客户端要求的信息或相应的错误代码。

WSD 扫描服务保留的作业历史记录量是特定于实现的。

此操作可以返回的所有[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。 有关如何对报告错误的详细信息，请参阅[WSD 扫描服务操作错误报告](wsd-scan-service-operation-error-reporting.md)。

<a name="examples"></a>示例
--------

下面的代码示例包含对作业历史记录的请求。

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
      http://schemas.microsoft.com/windows/2006/01/wdp/scan/GetJobHistory
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
  </soap:Header>

  <soap:Body>
    <wscn:GetJobHistoryRequest />
  </soap:Body>
</soap:Envelope>
```

## <a name="see-also"></a>另请参阅


[**GetJobHistoryResponse**](getjobhistoryresponse.md)

 

 






