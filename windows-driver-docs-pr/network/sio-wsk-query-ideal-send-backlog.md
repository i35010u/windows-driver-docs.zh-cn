---
title: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
description: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
ms.assetid: 8d05b1dc-9dbf-4726-9eaf-721d1fb8282e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_QUERY_IDEAL_SEND_BACKLOG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2a47bf3db1321bf8efdab1367165ff2d03121d64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576137"
---
# <a name="siowskqueryidealsendbacklog"></a>SIO\_WSK\_查询\_理想\_发送\_积压工作


SIO\_WSK\_查询\_理想\_发送\_积压工作套接字 I/O 控制操作允许查询面向连接的套接字的理想发送积压工作大小 WSK 应用程序。 此套接字的 I/O 控制操作仅适用于面向连接的套接字。

面向连接的套接字的理想之选的发送积压工作大小是最佳的需要保持未完成 （也就是说，传递给 WSK 子系统但尚未完成） 的发送数据量是为了保持完整的套接字的数据流在所有时间。 WSK 应用程序可以使用此大小以增量方式探测并锁定要基于基础连接的流控制状态发送数据的缓冲区。

如果 WSK 应用程序使用此套接字 I/O 控制操作查询的理想发送积压工作大小，它必须实现后的面向连接的套接字已连接到远程传输地址。

若要查询的面向连接的套接字的理想之选的发送积压工作大小，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_QUERY_IDEAL_SEND_BACKLOG</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(SIZE_T)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向一个 SIZE_T 类型的变量来接收当前理想发送积压工作大小</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数查询面向连接的套接字的理想之选的发送积压工作大小。

面向连接的套接字可以通过启用通知的理想发送积压工作大小更改其[ *WskSendBacklogEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff571147)事件回调函数。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




