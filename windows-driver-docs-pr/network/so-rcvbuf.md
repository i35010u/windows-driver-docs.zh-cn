---
title: SO_RCVBUF
description: SO_RCVBUF
ms.assetid: 218b52ac-95ee-4047-ad75-76d6ae6ab14e
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_RCVBUF 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f5d3f0aa519cabf2ca6abea464894258c8b1de66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841885"
---
# <a name="so_rcvbuf"></a>\_RCVBUF


SO\_RCVBUF 套接字选项确定基础传输使用的套接字接收缓冲区的大小。 此套接字选项仅适用于侦听套接字、数据报套接字和面向连接的套接字。

若要设置此 socket 选项的值，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p>SO_RCVBUF</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （ULONG）</p></td>
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
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

若要检索的值\_RCVBUF socket 选项，WSK 应用程序使用以下参数调用**WskControlSocket**函数。

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
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_RCVBUF</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
<td><p>SOL_SOCKET</p></td>
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
<td><p>sizeof （ULONG）</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收套接字的接收缓冲区的当前大小</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


调用**WskControlSocket**函数时，WSK 应用程序必须指定一个指向 IRP 的指针，以便设置或检索\_RCVBUF 套接字选项的值。

套接字的接收缓冲区的默认大小是特定于传输的。 某些传输可能不支持此套接字选项。

如果在侦听套接字上设置此套接字选项，则该侦听套接字上接受的所有传入连接都将其接收缓冲区设置为与为侦听套接字指定的大小相同的大小。 WSK 应用程序可以对已接受的套接字调用**WskControlSocket**函数，以覆盖从侦听套接字继承的接收缓冲区的大小。

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
<td>Ws2def （包括 Wsk）</td>
</tr>
</tbody>
</table>

 

 




