---
title: SIO_ADDRESS_LIST_QUERY
description: SIO_ADDRESS_LIST_QUERY
ms.assetid: c50520a3-6ba3-448e-bbb4-bf3425dcbc41
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_ADDRESS_LIST_QUERY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c34a4c04696aed1868b5f61686782339b9ed4314
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841914"
---
# <a name="sio_address_list_query"></a>SIO\_地址\_列表\_查询


SIO\_ADDRESS\_LIST\_查询套接字 i/o 控制操作允许 WSK 应用程序查询套接字地址系列的当前本地传输地址列表。 此套接字 i/o 控制操作适用于所有套接字类型。

若要查询套接字地址系列的本地传输地址的当前列表，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_ADDRESS_LIST_QUERY</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
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
<td><p><em>OutputBuffer</em>参数指向的缓冲区的大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向缓冲区的指针，该缓冲区接收本地传输地址的当前列表。 缓冲区的大小在<em>OutputSize</em>参数中指定。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收复制到<em>OutputBuffer</em>参数指向的缓冲区中的数据字节数。</p></td>
</tr>
</tbody>
</table>

 

在调用**WskControlSocket**函数来查询套接字地址系列的本地传输地址的当前列表时，WSK 应用程序不指定指向 IRP 的指针。

如果对**WskControlSocket**函数的调用成功，则输出缓冲区包含[**套接字\_地址\_列表**](https://docs.microsoft.com/windows/desktop/api/ws2def/ns-ws2def-_socket_address_list)结构，后跟套接字地址的每个本地传输地址的 SOCKADDR 结构全家.

如果**WskControlSocket**函数返回状态\_BUFFER\_溢出，则*OutputSizeReturned*参数指向的变量包含要包含完整列表所需的输出缓冲区大小（以字节为单位）。套接字地址系列的本地传输地址。

[**SIO\_地址\_列表\_更改**](sio-address-list-change.md)套接字 i/o 控制操作允许在对套接字地址系列的本地传输地址列表进行更改时通知 WSK 应用程序。

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

 

 




