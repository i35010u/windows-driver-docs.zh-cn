---
title: SIO_WSK_SET_SENDTO_ADDRESS
description: SIO_WSK_SET_SENDTO_ADDRESS
ms.assetid: 2dd149d2-adc6-4e03-92de-ed76aa048886
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_SET_SENDTO_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1d3b07421a412e53e6215f4b20546290e5669c19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351685"
---
# <a name="siowsksetsendtoaddress"></a>SIO\_WSK\_SET\_SENDTO\_ADDRESS


SIO\_WSK\_设置\_SENDTO\_地址套接字 I/O 控制操作允许 WSK 的应用程序来指定数据报套接字的固定的目标传输地址。 此套接字的 I/O 控制操作仅适用于数据报套接字。

如果 WSK 应用程序设置数据报套接字的固定的目标传输地址，通过套接字发送的所有数据报发送到固定的目标传输地址。 但是，数据报的套接字上接收将接受来自任何传输地址。

它通过套接字将数据报发送由指定替代远程传输地址中的时，WSK 应用程序可以重写固定的目标传输地址*RemoteAddress*参数调用时[**WskSendTo** ](https://msdn.microsoft.com/library/windows/hardware/ff571148)函数。 在这种情况下，数据报发送到备用远程传输地址而不是固定的目标传输地址。

如果 WSK 应用程序使用此套接字的 I/O 控制操作指定固定的目标传输地址，它必须实现后的数据报套接字已绑定到本地传输地址。

若要设置数据报套接字的固定的目标传输地址，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

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
<td><p>SIO_WSK_SET_SENDTO_ADDRESS</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>所指向的 SOCKADDR 结构的大小<em>InputBuffer</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向一个结构，指定数据报套接字的固定的目标传输地址的指针。 指针必须是指向特定对应于 WSK 应用程序指定在创建时的数据报套接字地址族的 SOCKADDR 结构类型的指针。</p></td>
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


若要清除的数据报套接字的固定的目标传输地址，WSK 应用程序调用**WskControlSocket**使用以下参数的函数。

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
<td><p>SIO_WSK_SET_SENDTO_ADDRESS</p></td>
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



WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数来设置或清除数据报套接字的固定的目标传输地址。

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

 

 




