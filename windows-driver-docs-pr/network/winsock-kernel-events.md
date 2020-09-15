---
title: Winsock 内核事件
description: Winsock 内核事件
ms.assetid: 84f7b547-cfbf-468b-b80e-1441c8aa3cf3
keywords:
- Winsock 内核 WDK 网络，事件
- WSK WDK 网络，事件
- 事件 WDK Winsock 内核
- 基本套接字 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 数据报套接字 WDK Winsock 内核
- 面向连接的套接字 WDK Winsock 内核
- 事件通知 WDK Winsock 内核
- 通知 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4dea6050ec9cecfd3d6b58b3e86f34c730e517
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101646"
---
# <a name="winsock-kernel-events"></a>Winsock 内核事件


Winsock 内核 (WSK) 子系统可以在发生某些套接字事件时（例如，当在套接字上收到新数据时，或者套接字已断开连接时）异步通知 WSK 应用程序。 若要为 WSK 应用程序异步通知套接字事件，WSK 应用程序必须实现相应的事件回调函数并在其创建的套接字上启用这些事件回调函数。

**注意**   WSK 应用程序不需要实现或使用事件回调函数。 WSK 应用程序可通过调用相应的 WSK 套接字函数来执行大多数 WSK 套接字操作。 需要使用事件回调函数的唯一 WSK 功能是侦听套接字上的条件-接受模式。 有关使用 WSK 函数与使用事件回调函数之间的优点和缺点的详细信息，请参阅 [使用 Winsock 内核函数与事件回调函数](using-winsock-kernel-functions-vs--event-callback-functions.md)。

 

每个 WSK [套接字类别](winsock-kernel-socket-categories.md) 都支持一组不同的套接字事件。

**基本套接字**

基本套接字不支持任何套接字事件。

**侦听套接字**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件</th>
<th align="left">事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>已接受传入连接。</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)"><em>WskAcceptEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>传入连接请求已收到。<em></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event" data-raw-source="[&lt;em&gt;WskInspectEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_inspect_event)"><em>WskInspectEvent</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>已删除传入连接请求。</em></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event" data-raw-source="[&lt;em&gt;WskAbortEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_abort_event)"><em>WskAbortEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

\* 仅适用于已启用条件接受模式的侦听套接字。 若要详细了解如何对侦听套接字使用条件接受模式，请参阅 [侦听和接受传入连接](listening-for-and-accepting-incoming-connections.md)。

**数据报套接字**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件</th>
<th align="left">事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>已收到一个或多个新的数据报。</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)"><em>WskReceiveFromEvent</em></a></p></td>
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
<th align="left">事件</th>
<th align="left">事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>已收到新数据。</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>套接字已断开连接。</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event)"><em>WskDisconnectEvent</em></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>理想的发送积压工作（backlog）大小已更改。</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>

 

当 WSK 应用程序创建套接字时，默认情况下将禁用套接字的事件回调函数。 WSK 应用程序必须启用套接字的事件回调函数，以便 WSK 子系统在出现套接字事件时调用套接字的事件回调函数。 有关启用和禁用套接字的事件回调函数的详细信息，请参阅 [启用和禁用事件回调函数](enabling-and-disabling-event-callback-functions.md)。

如果 WSK 应用程序为套接字注册 [扩展接口](winsock-kernel-extension-interfaces.md) ，扩展接口可能支持其他事件。 有关为套接字注册扩展接口的详细信息，请参阅 [注册扩展接口](registering-an-extension-interface.md)。

WSK 子系统还可以通知 WSK 应用程序不特定于特定套接字的事件。 为了让 WSK 应用程序收到这些事件的通知，WSK 应用程序必须实现 [*WskClientEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_client_event) 事件回调函数。 当前没有定义为特定于特定套接字的事件。 WSK 应用程序的 *WskClientEvent* 事件回调函数始终处于启用状态，并且无法禁用。

WSK 应用程序的事件回调函数不得等待 WSK 完成或事件回调函数上下文中其他 WSK 请求的完成。 回调可以启动其他 WSK 请求 (假设它在调度级别) 不会花费太多时间 \_ ，但它不能等待其完成，即使在 IRQL = 被动级别调用回调也是如此 \_ 。

