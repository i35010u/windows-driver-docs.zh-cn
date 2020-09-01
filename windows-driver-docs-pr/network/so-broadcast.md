---
title: SO_BROADCAST
description: SO_BROADCAST
ms.assetid: 24b93d4e-461d-44c3-b721-85cf41a1680a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_BROADCAST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7bbcc4d8b6df13a86c2b03f3b9fe5fd3e065e10d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205963"
---
# <a name="so_broadcast"></a>如此 \_ 广播


SO \_ 广播套接字选项的状态确定是否可以通过数据报套接字传输广播消息。 此套接字选项仅适用于数据报套接字。

若要设置此套接字选项的状态，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p>SO_BROADCAST</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量包含套接字选项的新状态值：</p>
<p>0：不允许广播消息</p>
<p>1：允许广播消息</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>

 

若要检索此 socket 选项的状态，WSK 应用程序需要使用以下参数调用 **WskControlSocket** 函数。

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
<td><p>SO_BROADCAST</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
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
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收 socket 选项的状态值：</p>
<p>0：不允许广播消息</p>
<p>1：允许广播消息</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>

 

WSK 应用程序在调用 **WskControlSocket** 函数时，必须指定一个指向 IRP 的指针，以便设置或检索 SO \_ 广播套接字选项的状态。

此套接字选项的默认状态是不允许广播消息。

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
<td>Ws2def (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

