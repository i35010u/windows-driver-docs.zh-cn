---
title: Bug 检查 0x156 WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP
description: WINSOCK_DETECTED_HUNG_CLOSESOCKET_LIVEDUMP bug 检查具有 0x00000156 值。 这表示 Winsock 检测到挂起的传输终结点关闭请求。
ms.assetid: F5B53149-3051-459C-834A-6AE17C56AEE6
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
ms.openlocfilehash: 99d2f912626b29977d10403e7e65f7574eb53aef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335555"
---
# <a name="bug-check-0x156-winsockdetectedhungclosesocketlivedump"></a>Bug 检查 0x156：WINSOCK\_已检测\_挂起\_套接字句\_LIVEDUMP


WINSOCK\_已检测\_挂起\_套接字句\_LIVEDUMP bug 检查的值为 0x00000156。 这表示 Winsock 检测到挂起的传输终结点关闭请求。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="winsockdetectedhungclosesocketlivedump-parameters"></a>WINSOCK\_已检测\_挂起\_套接字句\_LIVEDUMP 参数


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
<td align="left">AFD 终结点指针 (！ afdkd.endp &lt;ptr&gt;)</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>传输终结点类型</p>
<p>0x1:UDP 数据报</p>
<p>0x2:原始数据报</p>
<p>0x3:TCP 侦听器</p>
<p>0x4:TCP 终结点</p></td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">数据报终结点的缓冲的发送字节数</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">afd!NETIO_SUPER_TRIAGE_BLOCK</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

在处理关闭套接字请求时，Winsock 检测到挂起的传输终结点关闭请求。 系统生成的转储实时的分析，然后关闭套接字请求已完成而无需等待完成的挂起的传输终结点关闭请求。

 

 




