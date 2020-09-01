---
title: SIO_WSK_QUERY_INSPECT_ID
description: SIO_WSK_QUERY_INSPECT_ID
ms.assetid: 6fc3e5ea-61df-47fc-8f79-f9ae272b3544
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_QUERY_INSPECT_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 80987c9559c1fbecf5ad6e0245e9eeed41bc57f9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212759"
---
# <a name="sio_wsk_query_inspect_id"></a>SIO \_ WSK \_ 查询 \_ 检查 \_ ID


SIO \_ WSK \_ 查询 \_ 检查 \_ ID 套接字 I/O 控制操作允许 WSK 应用程序查询面向连接的套接字的检查标识数据，该套接字在启用条件接受模式的侦听套接字上已成功接受。 此套接字 i/o 控制操作仅适用于已在启用条件接受模式的侦听套接字上接受的面向连接的套接字。

若要查询面向连接的套接字的检查标识数据，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p>SIO_WSK_QUERY_INSPECT_ID</p></td>
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
<td><p>sizeof (WSK_INSPECT_ID) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向接收检查标识数据的 WSK_INSPECT_ID 结构的指针</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收复制到 <em>OutputBuffer</em> 参数指向的缓冲区中的数据字节数。</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>

如果 WSK 应用程序调用 **WskControlSocket** 函数来查询除面向连接的套接字之外的任何套接字的检查标识数据，而这些套接字在启用条件接受模式的侦听套接字上被接受，则 **WSKCONTROLSOCKET** 函数返回状态 " \_ 无效 \_ 设备 \_ 请求"。

有关有条件地接受连接的详细信息，请参阅 [侦听和接受传入连接](./listening-for-and-accepting-incoming-connections.md)。

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
<td>Wsk (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

