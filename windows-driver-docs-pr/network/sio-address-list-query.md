---
title: SIO_ADDRESS_LIST_QUERY
description: SIO_ADDRESS_LIST_QUERY
ms.assetid: c50520a3-6ba3-448e-bbb4-bf3425dcbc41
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_ADDRESS_LIST_QUERY 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: eb204b36ee0a88e7940b3dfb15df0bcb90e0eb2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380809"
---
# <a name="sioaddresslistquery"></a>SIO\_地址\_列表\_查询


SIO\_地址\_列表\_查询套接字 I/O 控制操作允许 WSK 的应用程序查询当前的套接字地址族的本地传输地址的列表。 此套接字的 I/O 控制操作适用于所有套接字类型。

若要查询的套接字地址族的本地传输地址的当前列表，WSK 应用程序调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)使用以下参数的函数。

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
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_ADDRESS_LIST_QUERY</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
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
<td><p>大小 （字节） 所指向的缓冲区<em>OutputBuffer</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向接收本地传输地址的当前列表的缓冲区的指针。 中指定的缓冲区的大小<em>OutputSize</em>参数。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向接收的数据复制到所指向的缓冲区的字节数的 ULONG 类型变量的指针<em>OutputBuffer</em>参数。</p></td>
</tr>
</tbody>
</table>

 

WSK 应用程序调用时未指定指向 IRP **WskControlSocket**函数查询当前的套接字地址族的本地传输地址的列表。

如果在调用**WskControlSocket**函数成功，则将在输出缓冲区中包含[**套接字\_地址\_列表**](https://docs.microsoft.com/windows/desktop/api/ws2def/ns-ws2def-_socket_address_list)结构为每个套接字的地址族的本地传输地址后跟 SOCKADDR 结构。

如果**WskControlSocket**函数将返回状态\_缓冲区\_溢出，所指向的变量*OutputSizeReturned*参数包含输出缓冲区大小 （字节），需包含的套接字地址族的本地传输地址的完整列表。

[ **SIO\_地址\_列表\_更改**](sio-address-list-change.md)套接字 I/O 控制操作允许 WSK 的应用程序时已到本地列表更改通知一个套接字地址族的传输地址。

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
<td>Ws2def.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




