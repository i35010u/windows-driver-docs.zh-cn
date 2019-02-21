---
title: 常见 WSD 扫描服务操作的错误代码
description: 本主题列出了是普遍适用于所有 WSD 扫描服务操作的错误代码。
ms.assetid: 138c29ff-5b2f-4145-95b0-4a9e8489bb37
keywords:
- 常见的 WSD 扫描服务操作错误代码成像设备
topic_type:
- apiref
api_name:
- Common WSD Scan Service Operation Error Codes
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f6c8c42831599b340ca4f26a96ac9777fc3dfb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525907"
---
# <a name="common-wsd-scan-service-operation-error-codes"></a>常见 WSD 扫描服务操作的错误代码


本主题列出了是普遍适用于所有 WSD 扫描服务操作的错误代码。 如果操作会导致多个错误，扫描服务应返回最具体的错误。

-   **Wsa:ActionNotSupported**

    当客户端请求的扫描服务不支持的操作时，WSD 扫描服务将返回此错误。

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
    <td><p>soap:Sender</p></td>
    </tr>
    <tr class="even">
    <td><p>[Subcode]</p></td>
    <td><p>wsa:ActionNotSupported</p></td>
    </tr>
    <tr class="odd">
    <td><p>[Reason]</p></td>
    <td><p>不能在接收方处理 [wsa:action]。</p></td>
    </tr>
    <tr class="even">
    <td><p>[详细信息]</p></td>
    <td><p><em>无效的操作名称</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **InvalidArgs**

    当客户端操作的一部分发送了无效的参数时，WSD 扫描服务将返回此错误。 无效的参数可能是以下任一项：

    -   没有足够*在*参数。
    -   有太多*在*参数。
    -   有没有*在*该名称的参数。
    -   一个或多个*在*参数都是错误的数据类型。

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
    <td><p>soap:Sender</p></td>
    </tr>
    <tr class="even">
    <td><p>[Subcode]</p></td>
    <td><p>wscn:InvalidArgs</p></td>
    </tr>
    <tr class="odd">
    <td><p>[Reason]</p></td>
    <td><p>至少一个输入的参数无效。</p></td>
    </tr>
    <tr class="even">
    <td><p>[详细信息]</p></td>
    <td><p><em>参数无效</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **OperationFailed**

    当扫描服务的当前状态阻止调用指定的操作时，WSD 扫描服务可以返回此错误。

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
    <td><p>soap:Receiver</p></td>
    </tr>
    <tr class="even">
    <td><p>[Subcode]</p></td>
    <td><p>wscn:OperationFailed</p></td>
    </tr>
    <tr class="odd">
    <td><p>[Reason]</p></td>
    <td><p>该服务无法执行请求的操作。</p></td>
    </tr>
    <tr class="even">
    <td><p>[详细信息]</p></td>
    <td><p><em>无</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **ServerErrorTemporaryError**

    服务器遇到临时错误而扫描程序正在处理该操作时，WSD 扫描服务将返回此错误。 客户端可以及时临时内部错误条件可能已清除的假定条件下尝试再次在以后某个时刻未经修改的请求。 如果没有更具体的错误定义适用于临时错误，例如磁盘已满，扫描服务应返回该错误代码。

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
    <td><p>soap:Receiver</p></td>
    </tr>
    <tr class="even">
    <td><p>[Subcode]</p></td>
    <td><p>wprt:ServerErrorTemporaryError</p></td>
    </tr>
    <tr class="odd">
    <td><p>[Reason]</p></td>
    <td><p>服务遇到意外的错误。</p></td>
    </tr>
    <tr class="even">
    <td><p>[详细信息]</p></td>
    <td><p><em>无</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **ServerErrorInternalError**

    当扫描程序遇到意外的情况而无法完成请求时，WSD 扫描服务将返回此错误。 此错误与不同**ServerErrorTemporaryError**在于这暗示着一更持久类型的内部错误并重新发送该操作将返回相同的容错。

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
    <td><p>soap:Receiver</p></td>
    </tr>
    <tr class="even">
    <td><p>[Subcode]</p></td>
    <td><p>wscn:ServerErrorInternalError</p></td>
    </tr>
    <tr class="odd">
    <td><p>[Reason]</p></td>
    <td><p>服务遇到意外的错误。</p></td>
    </tr>
    <tr class="even">
    <td><p>[详细信息]</p></td>
    <td><p><em>无</em></p></td>
    </tr>
    </tbody>
    </table>

     

 

 





