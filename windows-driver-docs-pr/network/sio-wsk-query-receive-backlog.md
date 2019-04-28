---
title: SIO_WSK_QUERY_RECEIVE_BACKLOG
description: SIO_WSK_QUERY_RECEIVE_BACKLOG
ms.assetid: 5924c6ae-fa9d-4a8c-acbe-65ca0664ad74
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_QUERY_RECEIVE_BACKLOG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ed4d02617201f39c6ebeb9f98d02ed52069d4edc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351698"
---
# <a name="siowskqueryreceivebacklog"></a>SIO\_WSK\_查询\_接收\_积压工作


SIO\_WSK\_查询\_接收\_积压工作套接字 I/O 控制操作允许查询的面向连接的套接字接收数据的当前积压 WSK 应用程序。 此套接字的 I/O 控制操作仅适用于面向连接的套接字。

如果 WSK 应用程序使用此套接字的 I/O 控制操作来查询接收积压工作，它必须实现后的面向连接的套接字已连接到远程传输地址。

若要查询的面向连接的套接字接收数据的当前积压，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

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
<td><p>SIO_WSK_QUERY_RECEIVE_BACKLOG</p></td>
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
<td><p>sizeof(SIZE_T)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向接收接收到的数据的当前积压 SIZE_T 类型变量的指针</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数查询面向连接的套接字接收数据的当前积压工作。

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

 

 




