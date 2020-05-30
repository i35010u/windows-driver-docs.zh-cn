---
title: WSD 扫描服务操作错误报告
description: WSD 扫描服务操作错误报告
ms.assetid: 78cf0cf9-f792-4dc9-b0df-c45b408b85ab
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: fed607d22461edf55d8bb4400490d13a5b53778a
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223516"
---
# <a name="wsd-scan-service-operation-error-reporting"></a>WSD 扫描服务操作错误报告

本部分介绍 WSD 扫描服务如何生成和发送操作错误代码。 [**常见的 WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)中介绍了大多数操作可以返回的错误代码。

当 WSD 扫描服务在处理*Xxx * * * 请求** 操作时遇到错误时，它将返回错误代码而不是*Xxx * * * Response** 元素。 扫描服务将返回** &lt; Soap： Fault &gt; **元素中的错误代码。

必须根据[Web 服务寻址（ws-addressing）规范](https://www.w3.org/Submission/ws-addressing/)中所述的规则发送在 WSD 扫描服务中定义的所有错误消息。 具体而言，WSD 扫描服务应将错误消息按顺序发送到以下位置：

1. \[ \] 如果存在且有效，则为错误终结点。

1. 否则为 \[ 答复终结点 \] （如果存在）。

1. 否则为 \[ 源终结点 \] 。

终结点必须在所有错误消息中包含所需的消息信息标头。 使用 \[ ws-addressing 中定义的关系属性将错误消息与响应相关联 \] 。 以下 \[ 操作 \] 属性指定错误消息：

```xml
https://schemas.xmlsoap.org/ws/2004/08/addressing/fault
```

错误的定义使用以下属性：

| 错误属性 | 定义 |
| --- | --- |
| 编写 | 错误代码。 |
| 子代码 | 错误子代码。 |
| 在于 | 英语 "原因" 元素。 |
| 仔细 | Detail 元素。 如果此元素不存在，则没有为错误定义详细信息元素。 |

这些属性绑定到 SOAP 1.2 错误，如下面的代码示例所示。

```xml
<S:Envelope>
  <S:Header>
    <wsa:Action>https://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
    <!-- Headers excluded for clarity -->
  </S:Header>
  <S:Body>
    <S:Fault>
      <S:Code>
        <S:Value>[Code]</S:Value>
        <S:Subcode>
          <S:Value>[Subcode]</S:Value>
        </S:Subcode>
      </S:Code>
      <S:Reason>
        <S:Text xml:lang="en">[Reason]</S:Text>
      </S:Reason>
      <S:Detail>[Detail]</S:Detail>
    </S:Fault>
  </S:Body>
</S:Envelope>
```

下面的代码示例演示了一个 SOAP**错误**示例。

```xml
<soap:Envelope xmlns:soap="https://www.w3.org/2003/05/soapelope"
    xmlns:xml="https://www.w3.org/XML/1998/namespace"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:nprt="https://schemas.microsoft.com/windows/2006/01/wdp/scan">
  <soap:Header>
    <wsa:Action>https://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
    <!-- Headers excluded for brevity -->
  </soap:Header>
  <soap:Body>
    <soap:Fault>
      <soap:Code>
        <soap:Value>env:Sender</soap:Value>
        <soap:Subcode>
          <soap:Value>wscn:OperationFailed</soap:Value>
        </soap:Subcode>
      </soap:Code>
      <soap:Reason>
        <soap:Text xml:lang="en">Service cannot perform the requested operation</soap:Text>
      </soap:Reason>
    </soap:Fault>
  </soap:Body>
</soap:Envelope>
```
