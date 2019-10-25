---
title: SO_WSK_EVENT_CALLBACK
description: SO_WSK_EVENT_CALLBACK
ms.assetid: cb697103-20ef-4667-8823-060a68d904c8
ms.date: 07/18/2017
keywords:
- SO_WSK_EVENT_CALLBACK 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8630f6f4c041dadae0874f22a2f81f54246bc2b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841879"
---
# <a name="so_wsk_event_callback"></a>因此\_WSK\_事件\_回调


因此\_WSK\_事件\_回调套接字选项允许 WSK 应用程序启用和禁用套接字的事件回调函数。 此套接字选项仅适用于侦听套接字、数据报套接字、面向连接的套接字和基本套接字，它们已注册至少为其定义了一个事件回调函数的扩展接口。

如果 WSK 应用程序使用此套接字选项启用或禁用侦听套接字或数据报套接字上的事件回调函数，则在套接字绑定到本地传输地址后，必须执行此操作。

如果 WSK 应用程序使用此套接字选项在面向连接的套接字上启用或禁用事件回调函数，则必须在套接字连接到远程传输地址后执行此操作。

若要启用或禁用套接字上的事件回调函数，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_WSK_EVENT_CALLBACK</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （WSK_EVENT_CALLBACK_CONTROL）</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)"><strong>WSK_EVENT_CALLBACK_CONTROL</strong></a>结构的指针</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


调用**WskControlSocket**函数在套接字上启用事件回调函数时，WSK 应用程序不指定指向 IRP 的指针。

在调用**WskControlSocket**函数来禁用套接字上的事件回调函数时，WSK 应用程序可以选择指定指向 IRP 的指针。

当 WSK 应用程序调用**WskControlSocket**来禁用事件回调函数时，WSK 子系统的行为如下所示：

-   如果在 WSK 应用程序调用**WskControlSocket**函数时，对正在禁用的事件回调函数进行正在进行的调用，则会禁用事件回调函数，并且**WSKCONTROLSOCKET**函数返回状态\_成功。 如果 WSK 应用程序指定了 IRP，则 IRP 已成功完成。

-   如果正在对事件回调函数进行正在进行的调用，而当 WSK 应用程序调用**WskControlSocket**函数，并且 WSK 应用程序指定了 IRP，则**WskControlSocket**函数将返回状态 @no__t_2未. 在对事件回调函数的所有正在进行的调用都返回后，WSK 子系统将禁用事件回调函数并完成 IRP。

-   如果在 WSK 应用程序调用**WskControlSocket**函数但 WSK 应用程序未指定 IRP 时要禁用事件回调函数的正在进行的调用，则**WSKCONTROLSOCKET**函数返回状态\_事件\_挂起。 在对事件回调函数进行的所有调用都返回后，WSK 子系统将禁用事件回调函数。

启用或禁用任何标准 WSK 事件回调函数时，WSK 应用程序会将 WSK\_事件的**NpiId**成员设置为指向 WSK 网络编程的指针[ **\_回调\_控制**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)结构[Interface （NPI）](https://docs.microsoft.com/windows-hardware/drivers/network/network-programming-interface) identifier、NPI\_WSK\_interface\_ID。

启用或禁用扩展接口的任何回调函数时，WSK 应用程序会将 WSK\_\_\_事件的**NpiId**成员设置为指向该扩展的 NPI 标识符的指针交互.

启用事件回调函数时，WSK 应用程序可以同时启用对特定[类别](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)的 WSK 套接字有效的事件回调函数的任意组合。 WSK 应用程序可通过将 WSK\_事件\_回调\_控制结构的**EventMask**成员设置为所有事件回调函数的按位 "或"，来同时启用这些组合。正在启用。

禁用事件回调函数时，WSK 应用程序必须独立禁用每个事件回调函数。 WSK 应用程序通过将 WSK\_事件\_回调\_控制结构的**EventMask**成员设置为事件回调函数的按位 "或" （作为已禁用并且 WSK\_事件\_禁用标志。

下表显示了侦听套接字的有效事件标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件标志</th>
<th>事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_ACCEPT</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)"><em>WskAcceptEvent</em></a></p></td>
</tr>
</tbody>
</table>


下表显示了数据报套接字的有效事件标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件标志</th>
<th>事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_RECEIVE_FROM</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_from_event)"><em>WskReceiveFromEvent</em></a></p></td>
</tr>
</tbody>
</table>



下表显示面向连接的套接字的有效事件标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件标志</th>
<th>事件回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_DISCONNECT</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect_event)"><em>WskDisconnectEvent</em></a></p></td>
</tr>
<tr class="even">
<td><p>WSK_EVENT_RECEIVE</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="odd">
<td><p>WSK_EVENT_SEND_BACKLOG</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_backlog_event)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>


在侦听套接字接受的面向连接的套接字上，侦听套接字可以自动启用事件回调函数。 WSK 应用程序通过在侦听套接字上启用面向连接的套接字事件回调函数，自动启用这些回调函数。 仅当侦听套接字的[*WskAcceptEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)事件回调函数接受套接字时，才会在已接受的面向连接的套接字上自动启用事件回调函数。 如果侦听套接字的[**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)函数接受面向连接的套接字，则不会自动启用接受的套接字的事件回调函数。

在侦听套接字上启用任何面向连接的事件回调函数后，将无法在侦听套接字上禁用它们。 如果在侦听套接字上禁用并重新启用*WskAcceptEvent*事件回调函数，则在该侦听套接字上最初启用的任何面向连接的事件回调函数都将继续应用于所有*WskAcceptEvent*事件回调函数接受的面向连接的套接字。

有关启用和禁用套接字的事件回调函数的详细信息，请参阅[启用和禁用事件回调函数](https://docs.microsoft.com/windows-hardware/drivers/network/enabling-and-disabling-event-callback-functions)。

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
<td>Wsk （包括 Wsk）</td>
</tr>
</tbody>
</table>

 

 




