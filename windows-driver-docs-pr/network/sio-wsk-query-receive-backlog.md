---
title: SIO_WSK_QUERY_RECEIVE_BACKLOG
description: SIO_WSK_QUERY_RECEIVE_BACKLOG
ms.assetid: 5924c6ae-fa9d-4a8c-acbe-65ca0664ad74
ms.date: 07/18/2017
keywords:
- SIO_WSK_QUERY_RECEIVE_BACKLOG 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 07896d59c9c2255d2e09bbc325bf5a04dde67f6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841901"
---
# <a name="sio_wsk_query_receive_backlog"></a>SIO\_WSK\_查询\_接收\_积压


SIO\_WSK\_QUERY\_RECEIVE\_积压工作套接字 i/o 控制操作允许 WSK 应用程序查询面向连接的套接字的已接收数据的当前积压。 此套接字 i/o 控制操作仅适用于面向连接的套接字。

如果 WSK 应用程序使用此套接字 i/o 控制操作来查询接收积压工作（backlog），则在面向连接的套接字连接到远程传输地址之后，必须执行此操作。

若要查询面向连接的套接字的已接收数据的当前积压，WSK 应用程序使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p>SIO_WSK_QUERY_RECEIVE_BACKLOG</p></td>
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
<td><p>sizeof （SIZE_T）</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 SIZE_T 类型的变量的指针，该变量接收接收的数据的当前积压</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

在调用**WskControlSocket**函数来查询面向连接的套接字的已接收数据的当前积压工作时，WSK 应用程序必须指定一个指向 IRP 的指针。

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

 

 




