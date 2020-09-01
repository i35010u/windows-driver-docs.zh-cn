---
title: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
description: SIO_WSK_QUERY_IDEAL_SEND_BACKLOG
ms.assetid: 8d05b1dc-9dbf-4726-9eaf-721d1fb8282e
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_QUERY_IDEAL_SEND_BACKLOG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 508427b31f09c896586beebaccd4d458f0f752bc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212763"
---
# <a name="sio_wsk_query_ideal_send_backlog"></a>SIO \_ WSK \_ 查询 \_ 理想的 \_ 发送 \_ 积压


SIO \_ WSK \_ 查询理想的 " \_ \_ 发送 \_ 积压工作套接字 I/O 控制" 操作允许 WSK 应用程序查询面向连接的套接字的理想发送积压工作（backlog）大小。 此套接字 i/o 控制操作仅适用于面向连接的套接字。

面向连接的套接字的理想发送积压工作（backlog）大小是需要保持未处理 (的最佳发送数据量，这些数据将被传递到 WSK 子系统但尚未完成) 使套接字的数据流始终保持满。 WSK 应用程序可使用此大小以增量方式探测和锁定要基于基础连接的流控制状态发送的数据缓冲区。

如果 WSK 应用程序使用此套接字 i/o 控制操作来查询理想的发送积压工作（backlog）大小，则必须在面向连接的套接字连接到远程传输地址后执行此操作。

若要查询面向连接的套接字的理想发送积压工作（backlog）大小，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p><em>级别</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (SIZE_T) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 SIZE_T 类型化的变量的指针，该变量接收当前的理想发送积压工作（backlog）大小</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>

调用 **WskControlSocket** 函数时，WSK 应用程序必须指定一个指向 IRP 的指针，以查询面向连接的套接字的理想发送积压工作（backlog）大小。

通过启用面向连接的套接字，可以通过启用其 [*WskSendBacklogEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event) 事件回调功能，通知对理想发送积压工作（backlog）大小的更改。

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
<td><p>标头</p></td>
<td>Wsk (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

