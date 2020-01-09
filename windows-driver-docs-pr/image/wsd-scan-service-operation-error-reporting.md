---
title: WSD 扫描服务操作错误报告
description: WSD 扫描服务操作错误报告
ms.assetid: 78cf0cf9-f792-4dc9-b0df-c45b408b85ab
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77f375b2b2b672f314f6c9b7abb920707911f92c
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75653011"
---
# <a name="wsd-scan-service-operation-error-reporting"></a>WSD 扫描服务操作错误报告


本部分介绍 WSD 扫描服务如何生成和发送操作错误代码。 [**常见的 WSD 扫描服务操作错误代码**](common-wsd-scan-service-operation-error-codes.md)中介绍了大多数操作可以返回的错误代码。

当 WSD 扫描服务在处理*Xxx * * * 请求** 操作时遇到错误时，它将返回错误代码而不是*Xxx * * * Response** 元素。 扫描服务返回 **&lt;soap： Fault&gt;** 元素中的错误代码。

必须根据[Web 服务寻址（ws-addressing）规范](https://go.microsoft.com/fwlink/p/?linkid=70144)中所述的规则发送在 WSD 扫描服务中定义的所有错误消息。 具体而言，WSD 扫描服务应将错误消息按顺序发送到以下位置：

1.  如果存在且有效，\[错误终结点\]。

2.  否则，\[回复终结点\]（如果存在）。

3.  否则，\[源终结点\]。

终结点必须在所有错误消息中包含所需的消息信息标头。 使用 WS-ADDRESSING 中定义的 \[关系\] 属性将错误消息与响应相关联。 以下 \[操作\] 属性指定错误消息：

```xml
https://schemas.xmlsoap.org/ws/2004/08/addressing/fault
```

错误的定义使用以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>错误属性</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>编写</p></td>
<td><p>错误代码。</p></td>
</tr>
<tr class="even">
<td><p>子代码</p></td>
<td><p>错误子代码。</p></td>
</tr>
<tr class="odd">
<td><p>在于</p></td>
<td><p>英语 "原因" 元素。</p></td>
</tr>
<tr class="even">
<td><p>仔细</p></td>
<td><p>Detail 元素。 如果此元素不存在，则没有为错误定义详细信息元素。</p></td>
</tr>
</tbody>
</table>

 

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

 

 





