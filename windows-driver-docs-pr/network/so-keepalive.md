---
title: SO_KEEPALIVE
description: SO_KEEPALIVE
ms.assetid: 47b29218-f227-4d36-b206-d8bf009252c0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_KEEPALIVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ea6dc1c84d48b2c0daae9e315c8703ed45cbcffb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543308"
---
# <a name="sokeepalive"></a>因此\_KEEPALIVE


SO 的状态\_KEEPALIVE 套接字选项用于确定是否在面向连接的套接字上发送保持活动状态的数据包。 此套接字选项仅适用于侦听套接字和面向连接的套接字。

若要设置此套接字选项的状态，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

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
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_KEEPALIVE</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向包含套接字选项的新状态的值的 ULONG 类型变量的指针：</p>
<ul>
<li><p>0:禁止发送保持活动数据包</p></li>
<li><p>1：启用发送保持活动状态的数据包</p></li>
</ul></td>
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



若要检索此套接字选项的状态，WSK 应用程序调用**WskControlSocket**使用以下参数的函数。

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
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_KEEPALIVE</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
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
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向一个 ULONG 类型的变量来接收套接字选项的状态的值的指针：</p>
<ul>
<li><p>0:发送保持活动状态的数据包被禁用</p></li>
<li><p>1：启用发送保持活动数据包</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数来设置或检索的状态等\_KEEPALIVE 套接字选项。

此套接字选项的默认状态是禁用发送保持活动状态的数据包。

如果在侦听套接字上启用了此套接字选项，则接受该侦听套接字的所有传入连接具有默认情况下启用此套接字选项。 WSK 应用程序可以调用**WskControlSocket**函数接受的套接字重写继承自侦听套接字时此套接字选项的状态。

基础网络传输发送保持活动数据包。 并非所有网络传输都支持发送保持活动状态的数据包。

有关使用 keep-alive 数据包的详细信息，请参阅*RFC 1122*，部分 4.2.3.6，"TCP Keep-alive"。

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
<td>Ws2def.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




