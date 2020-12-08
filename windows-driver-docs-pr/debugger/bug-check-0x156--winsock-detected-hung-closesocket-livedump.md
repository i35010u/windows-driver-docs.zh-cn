---
title: Bug 检查 0x156 WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
description: WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP bug 检查的值为0x00000156。 这表明 Winsock 检测到挂起的传输终结点关闭请求。
keywords:
- Bug 检查 0x156 WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
- WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6c0103d628c1a1cf6d8d6417b3dc074efa997a88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820975"
---
# <a name="bug-check-0x156-winsock_detected_hung_closesocket_livedump"></a>Bug 检查0x156： WINSOCK \_ 检测到 \_ 挂起 \_ 导致 \_ LIVEDUMP


WINSOCK \_ 检测到 \_ 挂起 \_ 导致 \_ LIVEDUMP bug 检查的值为0x00000156。 这表明 Winsock 检测到挂起的传输终结点关闭请求。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="winsock_detected_hung_closesocket_livedump-parameters"></a>WINSOCK \_ 检测到 \_ 挂起的 \_ 导致 \_ LIVEDUMP 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">AFD 终结点指针 (！ afdkd endp &lt; ptr &gt;) </td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>传输终结点类型</p>
<p>0x1： UDP 数据报</p>
<p>0x2：原始数据报</p>
<p>0x3： TCP 侦听器</p>
<p>0x4： TCP 终结点</p></td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">数据报终结点的缓冲发送字节数</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">afd!NETIO_SUPER_TRIAGE_BLOCK</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

处理导致请求时，Winsock 检测到挂起的传输终结点关闭请求。 系统生成了用于分析的实时转储，然后导致请求完成，而无需等待完成挂起的传输终结点关闭请求。

 

 




