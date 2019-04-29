---
title: SIO_WSK_QUERY_INSPECT_ID
description: SIO_WSK_QUERY_INSPECT_ID
ms.assetid: 6fc3e5ea-61df-47fc-8f79-f9ae272b3544
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_QUERY_INSPECT_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 07e89fe2c4ace3a6fa4c90ac7ca1bf427cb71119
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377229"
---
# <a name="siowskqueryinspectid"></a>SIO\_WSK\_查询\_检查\_ID


SIO\_WSK\_查询\_检查\_ID 套接字 I/O 控制操作允许 WSK 的应用程序查询已成功接受一个面向连接的套接字的检查标识数据有条件的侦听套接字接受已启用模式。 此套接字的 I/O 控制操作仅适用于面向连接的套接字上侦听的套接字具有条件接受启用模式接受。

若要查询的面向连接的套接字检查验证数据，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

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
<td><p>SIO_WSK_QUERY_INSPECT_ID</p></td>
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
<td><p>sizeof(WSK_INSPECT_ID)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向接收检测标识数据 WSK_INSPECT_ID 结构的指针</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向接收的数据复制到所指向的缓冲区的字节数的 ULONG 类型变量的指针<em>OutputBuffer</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

如果 WSK 应用程序调用**WskControlSocket**函数来查询非面向连接的套接字上侦听的套接字具有条件已接受的任何套接字的检查标识数据接受模式已启用， **WskControlSocket**函数将返回状态\_无效\_设备\_请求。

有关有条件地接受连接的详细信息，请参阅[用于侦听和接受传入连接](https://msdn.microsoft.com/library/windows/hardware/ff557059)。

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

 

 




