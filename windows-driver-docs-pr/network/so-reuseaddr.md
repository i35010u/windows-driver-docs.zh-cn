---
title: SO_REUSEADDR
description: SO_REUSEADDR
ms.assetid: 9436492b-0bfb-4234-bcf3-c44657a846d7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_REUSEADDR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 041884abb365ec731c2930064398129528d23eee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341387"
---
# <a name="soreuseaddr"></a>因此\_REUSEADDR


SO 的状态\_REUSEADDR 套接字选项用于确定是否要使用其他套接字始终共享套接字将绑定到的本地传输地址。 此套接字选项仅适用于侦听套接字、 数据报套接字和面向连接的套接字。

如果 WSK 应用程序将此套接字选项，则它必须实现之前接字绑定到本地传输地址。

若要设置此套接字选项的状态，WSK 应用程序调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)使用以下参数的函数。

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
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_REUSEADDR</p></td>
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
<li><p>0:禁用始终共享本地传输地址</p></li>
<li><p>1：启用始终共享本地传输地址</p></li>
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
<td><p>SO_REUSEADDR</p></td>
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
<li><p>0:始终共享本地传输地址已禁用</p></li>
<li><p>1：启用了始终共享本地传输地址</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数来设置或检索的状态等\_REUSEADDR 套接字选项。

此套接字选项的默认状态是禁用始终共享本地传输地址。

详细了解使用 SO\_REUSEADDR 套接字选项和其影响上共享本地传输地址之间套接字，请参阅[共享传输地址](https://msdn.microsoft.com/library/windows/hardware/ff570806)。

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

 

 




