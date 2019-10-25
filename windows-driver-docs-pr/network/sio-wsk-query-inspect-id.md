---
title: SIO_WSK_QUERY_INSPECT_ID
description: SIO_WSK_QUERY_INSPECT_ID
ms.assetid: 6fc3e5ea-61df-47fc-8f79-f9ae272b3544
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_INSPECT_ID 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d68c55d59af6b4e7a021218042df701a6f0d08b3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841903"
---
# <a name="sio_wsk_query_inspect_id"></a>SIO\_WSK\_QUERY\_检查\_ID


SIO\_WSK\_QUERY\_检查\_ID 套接字 i/o 控制操作是否允许 WSK 应用程序查询面向连接的套接字的检查标识数据，该套接字在已启用条件接受模式。 此套接字 i/o 控制操作仅适用于已在启用条件接受模式的侦听套接字上接受的面向连接的套接字。

若要查询面向连接的套接字的检查标识数据，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p>SIO_WSK_QUERY_INSPECT_ID</p></td>
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
<td><p>sizeof （WSK_INSPECT_ID）</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 WSK_INSPECT_ID 结构的指针，该结构接收检查标识数据</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收复制到<em>OutputBuffer</em>参数指向的缓冲区中的数据字节数。</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

如果 WSK 应用程序调用**WskControlSocket**函数来查询除面向连接的套接字之外的任何套接字的检查标识数据，该套接字在已启用条件接受模式的侦听套接字上被接受， **WskControlSocket**函数返回\_无效\_设备\_请求的状态。

有关有条件地接受连接的详细信息，请参阅[侦听和接受传入连接](https://docs.microsoft.com/windows-hardware/drivers/network/listening-for-and-accepting-incoming-connections)。

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

 

 




