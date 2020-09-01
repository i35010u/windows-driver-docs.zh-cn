---
title: SO_RCVBUF
description: SO_RCVBUF
ms.assetid: 218b52ac-95ee-4047-ad75-76d6ae6ab14e
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_RCVBUF 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1188ce957d9d05d85088bef0b67908aa98137a3e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205951"
---
# <a name="so_rcvbuf"></a>\_RCVBUF


SO \_ RCVBUF socket 选项确定了基础传输使用的套接字接收缓冲区的大小。 此套接字选项仅适用于侦听套接字、数据报套接字和面向连接的套接字。

若要设置此 socket 选项的值，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_RCVBUF</p></td>
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
<td><p>指向一个 ULONG 类型的变量的指针，该变量包含套接字的接收缓冲区的新大小</p></td>
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

若要检索 \_ RCVBUF socket 选项的值，WSK 应用程序使用以下参数调用 **WskControlSocket** 函数。

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
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_RCVBUF</p></td>
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
<td><p>指向 ULONG 类型的变量的指针，该变量接收套接字的接收缓冲区的当前大小</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>


调用 **WskControlSocket** 函数时，WSK 应用程序必须指定一个指向 IRP 的指针，以便设置或检索 SO \_ RCVBUF 套接字选项的值。

套接字的接收缓冲区的默认大小是特定于传输的。 某些传输可能不支持此套接字选项。

如果在侦听套接字上设置此套接字选项，则该侦听套接字上接受的所有传入连接都将其接收缓冲区设置为与为侦听套接字指定的大小相同的大小。 WSK 应用程序可以对已接受的套接字调用 **WskControlSocket** 函数，以覆盖从侦听套接字继承的接收缓冲区的大小。

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

 

