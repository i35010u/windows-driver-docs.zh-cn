---
title: SO_REUSEADDR
description: SO_REUSEADDR
ms.assetid: 9436492b-0bfb-4234-bcf3-c44657a846d7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_REUSEADDR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 16ef2c72eb95a26171788c22eee6b4a7c953515b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841881"
---
# <a name="so_reuseaddr"></a>\_REUSEADDR


SO\_REUSEADDR 套接字选项的状态决定了将套接字绑定到的本地传输地址是否始终与其他套接字共享。 此套接字选项仅适用于侦听套接字、数据报套接字和面向连接的套接字。

如果 WSK 应用程序设置此套接字选项，则必须在将套接字绑定到本地传输地址之前执行此操作。

若要设置此套接字选项的状态，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_REUSEADDR</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （ULONG）</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量包含套接字选项的新状态值：</p>
<ul>
<li><p>0：禁用始终共享本地传输地址</p></li>
<li><p>1：允许始终共享本地传输地址</p></li>
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

若要检索此 socket 选项的状态，WSK 应用程序需要使用以下参数调用**WskControlSocket**函数。

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
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_REUSEADDR</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
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
<td><p>sizeof （ULONG）</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收 socket 选项的状态值：</p>
<ul>
<li><p>0：始终共享本地传输地址已禁用</p></li>
<li><p>1：始终共享本地传输地址已启用</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

WSK 应用程序必须在调用**WskControlSocket**函数时指定一个指向 IRP 的指针，以便设置或检索\_REUSEADDR 套接字选项的状态。

此套接字选项的默认状态是 "始终共享本地传输地址" 处于禁用状态。

若要详细了解如何使用\_REUSEADDR 套接字选项及其对套接字间本地传输地址的影响，请参阅[共享传输地址](https://docs.microsoft.com/windows-hardware/drivers/network/sharing-transport-addresses)。

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

 

 




