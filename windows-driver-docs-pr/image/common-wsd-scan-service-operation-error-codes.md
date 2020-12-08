---
title: 常见 WSD 扫描服务操作错误代码
description: 本主题列出了所有 WSD 扫描服务操作共有的错误代码。
keywords:
- 常见的 WSD 扫描服务操作错误代码图像处理设备
topic_type:
- apiref
api_name:
- Common WSD Scan Service Operation Error Codes
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7721eaf74cc29e4e7dddbf9fd516869fd67121d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823175"
---
# <a name="common-wsd-scan-service-operation-error-codes"></a>常见 WSD 扫描服务操作错误代码


本主题列出了所有 WSD 扫描服务操作共有的错误代码。 如果某个操作导致多个错误，则扫描服务应返回最具体的错误。

-   **Wsa： ActionNotSupported**

    当客户端请求扫描服务不支持的操作时，WSD 扫描服务将返回此错误。

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
    <td><p>soap：发送方</p></td>
    </tr>
    <tr class="even">
    <td><p>子代码</p></td>
    <td><p>wsa:ActionNotSupported</p></td>
    </tr>
    <tr class="odd">
    <td><p>在于</p></td>
    <td><p>不能在接收方处理 [wsa： action]。</p></td>
    </tr>
    <tr class="even">
    <td><p>仔细</p></td>
    <td><p><em>无效的操作名称</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **InvalidArgs**

    当客户端发送无效参数作为操作的一部分时，WSD 扫描服务将返回此错误。 无效参数可以是以下任一项：

    -   没有足够 *的 in* 参数。
    -   *参数太* 多。
    -   该名称中不存在 *in* 参数。
    -   一个或多个 *in* 参数的数据类型不正确。

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
    <td><p>soap：发送方</p></td>
    </tr>
    <tr class="even">
    <td><p>子代码</p></td>
    <td><p>wscn:InvalidArgs</p></td>
    </tr>
    <tr class="odd">
    <td><p>在于</p></td>
    <td><p>至少一个输入参数无效。</p></td>
    </tr>
    <tr class="even">
    <td><p>仔细</p></td>
    <td><p><em>无效参数</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **OperationFailed**

    当扫描服务的当前状态阻止调用指定操作时，WSD 扫描服务可以返回此错误。

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
    <td><p>soap：接收方</p></td>
    </tr>
    <tr class="even">
    <td><p>子代码</p></td>
    <td><p>wscn:OperationFailed</p></td>
    </tr>
    <tr class="odd">
    <td><p>在于</p></td>
    <td><p>服务无法执行请求的操作。</p></td>
    </tr>
    <tr class="even">
    <td><p>仔细</p></td>
    <td><p><em>无</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **ServerErrorTemporaryError**

    当扫描程序正在处理操作时，如果服务器遇到暂时性错误，WSD 扫描服务将返回此错误。 客户端可以在以后的某个时间点再次尝试未修改的请求，因为可能已清除了暂时的内部错误条件。 如果定义了一个适用于临时错误的更具体的错误，例如磁盘已满，则扫描服务应返回该错误代码。

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
    <td><p>soap：接收方</p></td>
    </tr>
    <tr class="even">
    <td><p>子代码</p></td>
    <td><p>wprt:ServerErrorTemporaryError</p></td>
    </tr>
    <tr class="odd">
    <td><p>在于</p></td>
    <td><p>服务出现错误。</p></td>
    </tr>
    <tr class="even">
    <td><p>仔细</p></td>
    <td><p><em>无</em></p></td>
    </tr>
    </tbody>
    </table>

     

-   **ServerErrorInternalError**

    当扫描程序遇到阻止其完成请求的意外情况时，WSD 扫描服务将返回此错误。 此错误与 **ServerErrorTemporaryError** 的不同之处在于，它表示存在更永久性的内部错误类型，重新发送操作将返回相同的错误。

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
    <td><p>soap：接收方</p></td>
    </tr>
    <tr class="even">
    <td><p>子代码</p></td>
    <td><p>wscn:ServerErrorInternalError</p></td>
    </tr>
    <tr class="odd">
    <td><p>在于</p></td>
    <td><p>服务出现错误。</p></td>
    </tr>
    <tr class="even">
    <td><p>仔细</p></td>
    <td><p><em>无</em></p></td>
    </tr>
    </tbody>
    </table>

     

 

 





