---
title: SO_KEEPALIVE
description: SO_KEEPALIVE
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_KEEPALIVE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d58ff5bb9b2167ad7ed89b59df68028a20c3be03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824999"
---
# <a name="so_keepalive"></a>所以 \_ KEEPALIVE


" \_ 生存套接字" 选项的状态确定是否在面向连接的套接字上发送 "keep-alive" 数据包。 此套接字选项仅适用于侦听套接字和面向连接的套接字。

若要设置此套接字选项的状态，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_KEEPALIVE</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量包含套接字选项的新状态值：</p>
<ul>
<li><p>0：禁用发送保持活动状态的数据包</p></li>
<li><p>1：启用发送保持活动状态的数据包</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>



若要检索此 socket 选项的状态，WSK 应用程序需要使用以下参数调用 **WskControlSocket** 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_KEEPALIVE</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
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
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收 socket 选项的状态值：</p>
<ul>
<li><p>0：已禁用发送保持活动状态的数据包</p></li>
<li><p>1：已启用 keep-alive 数据包发送</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>


WSK 应用程序必须在调用 **WskControlSocket** 函数时指定一个指向 IRP 的指针，以便设置或检索 SO \_ KEEPALIVE 套接字选项的状态。

此套接字选项的默认状态是禁用 "保持活动" 数据包。

如果在侦听套接字上启用了此套接字选项，则该侦听套接字上接受的所有传入连接都默认启用此套接字选项。 WSK 应用程序可以对已接受的套接字调用 **WskControlSocket** 函数，以覆盖从侦听套接字继承的此套接字选项的状态。

保持活动状态的数据包由基础网络传输来发送。 并非所有网络传输都支持发送保持活动状态的数据包。

有关使用 keep-alive 数据包的详细信息，请参阅 *RFC 1122* 4.2.3.6 "TCP 保持连接" 一节。

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
<td>Ws2def (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

