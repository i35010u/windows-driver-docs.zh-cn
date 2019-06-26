---
title: Winsock 内核事件
description: Winsock 内核事件
ms.assetid: 84f7b547-cfbf-468b-b80e-1441c8aa3cf3
keywords:
- 网络、 Winsock 内核 WDK 事件
- WSK WDK 网络、 事件
- 事件 WDK Winsock 内核
- 基本套接字 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 数据报套接字 WDK Winsock 内核
- 面向连接的套接字 WDK Winsock 内核
- 事件通知 WDK Winsock 内核
- 通知 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8cfb17185f161dfeb061602eb7e4d848102a3f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360226"
---
# <a name="winsock-kernel-events"></a>Winsock 内核事件


发生特定套接字事件，例如当新数据已接收套接字或当套接字已断开连接时，Winsock Kernel (WSK) 子系统可以以异步方式通知 WSK 应用程序。 为了使 WSK 应用程序以异步方式接收套接字的事件通知，WSK 应用程序必须实现相应的事件回调函数，并启用它创建的套接字上这些事件回调函数。

**请注意**  WSK 应用程序不需要实现或使用事件回调函数。 WSK 应用程序可以通过调用适当的 WSK 套接字函数执行大多数 WSK 套接字操作。 需要使用事件回调函数是唯一 WSK 功能条件接受侦听套接字上的模式。 有关使用 WSK 函数与使用事件的回调函数之间的优缺点的详细信息，请参阅[使用 Winsock 内核函数 vs。事件回调函数](using-winsock-kernel-functions-vs--event-callback-functions.md)。

 

每个 WSK[套接字类别](winsock-kernel-socket-categories.md)支持一组不同的套接字的事件。

**基本的套接字**

基本的套接字不支持任何套接字的事件。

**侦听套接字**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Event</th>
<th align="left">事件的回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>已接受传入连接。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event)"><em>WskAcceptEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>已到达的传入连接请求。<em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_inspect_event" data-raw-source="[&lt;em&gt;WskInspectEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_inspect_event)"><em>WskInspectEvent</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>已丢弃的传入连接请求。</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_abort_event" data-raw-source="[&lt;em&gt;WskAbortEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_abort_event)"><em>WskAbortEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

\* 仅适用于具有侦听套接字条件接受模式已启用。 有关使用条件性的详细信息接受与侦听套接字的模式，请参阅[用于侦听和接受传入连接](listening-for-and-accepting-incoming-connections.md)。

**数据报套接字**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Event</th>
<th align="left">事件的回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>接收的一个或多个新的数据报。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from_event" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from_event)"><em>WskReceiveFromEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

**面向连接的套接字**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Event</th>
<th align="left">事件的回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>已收到新数据。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>套接字已断开连接。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect_event" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect_event)"><em>WskDisconnectEvent</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>理想发送积压工作大小已更改。</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_backlog_event" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_backlog_event)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

当 WSK 应用程序创建套接字时，默认情况下禁用套接字的事件回调函数。 WSK 应用程序必须启用顺序为 WSK 子系统套接字的事件发生时调用的套接字的事件回调函数的套接字的事件回调函数。 有关启用和禁用套接字的事件回调函数的详细信息，请参阅[启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

如果注册了一个应用程序，WSK[扩展接口](winsock-kernel-extension-interfaces.md)套接字时，扩展接口可能支持其他事件。 有关注册一个套接字的一个扩展接口的详细信息，请参阅[注册一个扩展接口](registering-an-extension-interface.md)。

WSK 子系统还可以通知 WSK 应用程序并不特定于特定的套接字的事件。 为了使 WSK 应用程序以接收这些事件通知，WSK 应用程序必须实现[ *WskClientEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_client_event)事件回调函数。 有当前未定义的事件，并不特定于特定的套接字。 WSK 应用程序的*WskClientEvent*事件回叫函数始终处于启用状态并不能禁用。

WSK 应用程序的事件回调函数必须等待其他 WSK 请求 WSK 完成或事件回调函数的上下文中完成。 回调可以启动其他 WSK 请求 (假设它不会花太长时间在调度\_级别)，但它必须等待其完成的回调调用在 IRQL，即使 = 被动\_级别。

 

 





