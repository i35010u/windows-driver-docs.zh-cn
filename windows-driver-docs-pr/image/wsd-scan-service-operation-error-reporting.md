---
title: WSD 扫描服务操作错误报告
description: WSD 扫描服务操作错误报告
ms.assetid: 78cf0cf9-f792-4dc9-b0df-c45b408b85ab
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bf2e54facd2894bcd7320938b6a8ed971883371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555144"
---
# <a name="wsd-scan-service-operation-error-reporting"></a>WSD 扫描服务操作错误报告


本部分介绍如何 WSD 扫描服务生成并发送错误代码的操作。 大多数操作都可以返回的错误代码中所述[**常见 WSD 扫描服务操作的错误代码**](common-wsd-scan-service-operation-error-codes.md)。

WSD 扫描服务时遇到错误时处理*Xxx * * * 请求** 操作，它将返回错误代码而不是*Xxx * * * 响应** 元素。 扫描服务将返回中的错误代码 **&lt;soap： 错误&gt;** 元素。

必须根据中所述的规则发送 WSD 扫描服务中定义的所有错误消息[Web 服务寻址 (Ws-addressing) 规范](https://go.microsoft.com/fwlink/p/?linkid=70144)。 具体而言，WSD 扫描服务应将错误消息发送到以下位置顺序：

1.  \[容错终结点\]、 是否存在且有效。

2.  否则为\[答复终结点\]、 是否存在。

3.  否则为\[源终结点\]。

终结点必须包含必需的消息信息的所有错误消息的标头。 通过使用作为回复而关联错误消息\[关系\]Ws-addressing 中定义的属性。 以下\[操作\]属性指定错误消息：

```xml
http://schemas.xmlsoap.org/ws/2004/08/addressing/fault
```

错误进行的定义使用以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fault 属性</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[Code]</p></td>
<td><p>错误代码。</p></td>
</tr>
<tr class="even">
<td><p>[Subcode]</p></td>
<td><p>错误子代码。</p></td>
</tr>
<tr class="odd">
<td><p>[Reason]</p></td>
<td><p>英语语言原因元素。</p></td>
</tr>
<tr class="even">
<td><p>[详细信息]</p></td>
<td><p>详细信息元素中。 如果此元素不存在，没有详细信息元素定义的错误。</p></td>
</tr>
</tbody>
</table>

 

这些属性绑定到 SOAP 1.2 错误如以下代码示例所示。

```xml
<S:Envelope>
  <S:Header>
    <wsa:Action>http://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
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

下面的代码示例显示了示例 SOAP**容错**。

```xml
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soapelope"
    xmlns:xml="http://www.w3.org/XML/1998/namespace"
    xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:nprt="http://schemas.microsoft.com/windows/2006/01/wdp/scan">
  <soap:Header>
    <wsa:Action>http://schemas.xmlsoap.org/ws/2004/08/addressing/fault</wsa:Action>
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

 

 





