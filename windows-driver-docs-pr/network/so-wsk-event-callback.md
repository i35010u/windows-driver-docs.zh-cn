---
title: SO_WSK_EVENT_CALLBACK
description: SO_WSK_EVENT_CALLBACK
ms.assetid: cb697103-20ef-4667-8823-060a68d904c8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SO_WSK_EVENT_CALLBACK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 882d48d604b111fd3dd8daf1db76d9dba17267b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374747"
---
# <a name="sowskeventcallback"></a>因此\_WSK\_事件\_回调


SO\_WSK\_事件\_回调套接字选项允许 WSK 的应用程序启用和禁用套接字的事件回调函数。 此套接字选项仅适用于侦听套接字、 数据报套接字、 面向连接的套接字和基本的套接字的已注册为其定义至少一个事件回调函数的扩展接口。

如果 WSK 应用程序使用此套接字选项来启用或禁用在侦听套接字或数据报套接字上的事件回调函数，它必须实现后套接字已绑定到本地传输地址。

如果 WSK 应用程序使用此套接字选项来启用或禁用在面向连接的套接字上的事件回调函数，它必须实现后套接字已连接到远程传输地址。

若要启用或禁用对套接字的事件回调函数，WSK 应用程序调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>ReplTest1</th>
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
<td><p><em>Level</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_EVENT_CALLBACK_CONTROL)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>一个指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_event_callback_control" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_event_callback_control)"> <strong>WSK_EVENT_CALLBACK_CONTROL</strong> </a>结构</p></td>
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


WSK 应用程序调用时未指定指向 IRP **WskControlSocket**函数，以使套接字上的事件回调函数。

WSK 应用程序 （可选） 调用时指定一个指向 IRP **WskControlSocket**函数可禁用套接字上一个事件的回调函数。

当 WSK 程序调用**WskControlSocket**若要禁用了事件的回调函数，WSK 子系统的行为，如下所示：

-   如果有任何正在进行中调用 WSK 应用程序调用时，会被禁用事件回调函数**WskControlSocket**禁用函数，事件回调函数和**WskControlSocket**函数将返回状态\_成功。 如果 WSK 应用程序指定 IRP，IRP 是已完成，但成功状态。

-   如果有正在进行中调用 WSK 应用程序调用时，会被禁用事件回调函数**WskControlSocket**函数和 WSK 应用程序指定 IRP， **WskControlSocket**函数将返回状态\_PENDING。 WSK 子系统禁用事件回调函数，并完成 IRP 之后返回到事件的回调函数的所有正在进行中调用。

-   如果有正在进行中调用 WSK 应用程序调用时，会被禁用事件回调函数**WskControlSocket**函数和 WSK 应用程序未指定 IRP， **WskControlSocket**函数将返回状态\_事件\_PENDING。 WSK 子系统禁用事件回调函数后返回所有正在进行中调用事件回调函数。

WSK 应用程序时启用或禁用的任何标准 WSK 事件回调函数时，设置**NpiId**的成员[ **WSK\_事件\_回调\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_event_callback_control)结构为指向 WSK[网络编程接口 (NPI)](https://docs.microsoft.com/windows-hardware/drivers/network/network-programming-interface)标识符，NPI\_WSK\_接口\_id。

WSK 应用程序时启用或禁用扩展接口任何回调函数时，设置**NpiId** WSK 成员\_事件\_回调\_为指向 NPI 的控制结构该扩展插件接口的标识符。

WSK 应用程序时启用事件回调函数，可以同时启用适用于特定的事件回调函数的任意组合[类别](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)WSK 套接字。 WSK 应用程序通过设置同时使这些组合**EventMask** WSK 成员\_事件\_回调\_到所有的事件标志的按位 OR 的控制结构正在启用事件回调函数。

当禁用事件回调函数，WSK 应用程序必须单独禁用每个事件的回调函数。 WSK 应用程序单独通过设置禁用了事件的回调函数**EventMask** WSK 成员\_事件\_回调\_到的事件标志的按位 OR 的控制结构正在禁用的事件的回调函数和 WSK\_事件\_禁用标志。

下表显示了侦听套接字的有效的事件标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件标志</th>
<th>事件的回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_ACCEPT</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event" data-raw-source="[&lt;em&gt;WskAcceptEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event)"><em>WskAcceptEvent</em></a></p></td>
</tr>
</tbody>
</table>


下表显示了数据报套接字的有效的事件标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件标志</th>
<th>事件的回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_RECEIVE_FROM</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from_event" data-raw-source="[&lt;em&gt;WskReceiveFromEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_from_event)"><em>WskReceiveFromEvent</em></a></p></td>
</tr>
</tbody>
</table>



下表显示了一个面向连接的套接字的有效的事件标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件标志</th>
<th>事件的回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WSK_EVENT_DISCONNECT</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect_event" data-raw-source="[&lt;em&gt;WskDisconnectEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect_event)"><em>WskDisconnectEvent</em></a></p></td>
</tr>
<tr class="even">
<td><p>WSK_EVENT_RECEIVE</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event" data-raw-source="[&lt;em&gt;WskReceiveEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event)"><em>WskReceiveEvent</em></a></p></td>
</tr>
<tr class="odd">
<td><p>WSK_EVENT_SEND_BACKLOG</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_backlog_event" data-raw-source="[&lt;em&gt;WskSendBacklogEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send_backlog_event)"><em>WskSendBacklogEvent</em></a></p></td>
</tr>
</tbody>
</table>


侦听套接字可以自动启用面向连接的套接字，都可以接受的侦听套接字上的事件回调函数。 WSK 应用程序会自动启用这些回调函数，通过启用侦听套接字上的面向连接的套接字事件回调函数。 事件回调函数会自动启用已接受的面向连接的套接字上侦听套接字的套接字被接受，才[ *WskAcceptEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event)事件回调函数。 如果通过侦听套接字接受面向连接的套接字[ **WskAccept** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept)函数，接受套接字的事件回调函数不会自动启用。

在侦听套接字上启用任何面向连接的事件的回调函数后，它们不能禁用侦听套接字上。 如果*WskAcceptEvent* 、 事件的回调函数是禁用并重新启用侦听套接字上最初已启用该侦听套接字任何面向连接的事件回调函数将继续应用于所有面向连接的套接字接受*WskAcceptEvent*事件回调函数。

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
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




