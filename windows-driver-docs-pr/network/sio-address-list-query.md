---
title: SIO_ADDRESS_LIST_QUERY
description: SIO_ADDRESS_LIST_QUERY
ms.assetid: c50520a3-6ba3-448e-bbb4-bf3425dcbc41
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_ADDRESS_LIST_QUERY 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b413431bec3ef31c25eef28b2b3d7e79939e33d7
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715520"
---
# <a name="sio_address_list_query"></a>SIO \_ 地址 \_ 列表 \_ 查询


SIO \_ ADDRESS \_ LIST \_ QUERY socket i/o CONTROL 操作允许 WSK 应用程序查询套接字地址系列的当前本地传输地址列表。 此套接字 i/o 控制操作适用于所有套接字类型。

若要查询套接字地址系列的本地传输地址的当前列表，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p>SIO_ADDRESS_LIST_QUERY</p></td>
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
<td><p><em>OutputBuffer</em>参数指向的缓冲区的大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向缓冲区的指针，该缓冲区接收本地传输地址的当前列表。 缓冲区的大小在 <em>OutputSize</em> 参数中指定。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收复制到 <em>OutputBuffer</em> 参数指向的缓冲区中的数据字节数。</p></td>
</tr>
</tbody>
</table>

 

在调用 **WskControlSocket** 函数来查询套接字地址系列的本地传输地址的当前列表时，WSK 应用程序不指定指向 IRP 的指针。

如果对 **WskControlSocket** 函数的调用成功，则输出缓冲区包含 [**套接字 \_ 地址 \_ 列表**](/windows/win32/api/ws2def/ns-ws2def-_socket_address_list) 结构，后跟套接字地址系列的每个本地传输地址的 SOCKADDR 结构。

如果 **WskControlSocket** 函数返回状态 \_ 缓冲区 \_ 溢出，则由 *OutputSizeReturned* 参数指向的变量包含的输出缓冲区大小（以字节为单位），该大小需要包含套接字地址系列的本地传输地址的完整列表。

[**SIO \_ 地址 \_ 列表 \_ 更改**](sio-address-list-change.md)套接字 i/o 控制操作允许在对套接字地址系列的本地传输地址列表进行更改时通知 WSK 应用程序。

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

 

