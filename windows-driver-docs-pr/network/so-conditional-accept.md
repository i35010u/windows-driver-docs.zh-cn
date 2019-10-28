---
title: SO_CONDITIONAL_ACCEPT
description: SO_CONDITIONAL_ACCEPT
ms.assetid: 8aaaa08b-b239-4648-8c4f-8db2efbda551
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_CONDITIONAL_ACCEPT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e25f085704b9d48e99beed0c62a6bc3934a437ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841893"
---
# <a name="so_conditional_accept"></a>因此\_条件\_接受


SO\_条件\_ACCEPT socket 选项的状态确定是否在侦听套接字上启用条件接受模式。 此套接字选项仅适用于侦听套接字。

如果 WSK 应用程序设置此套接字选项，则必须在侦听套接字绑定到本地传输地址之前执行此操作。

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
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
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
<p>0：禁用条件接受模式</p>
<p>1：启用条件接受模式</p></td>
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
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
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
<p>0：已禁用条件接受模式</p>
<p>1：条件接受模式已启用</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>



调用**WskControlSocket**函数时，WSK 应用程序必须指定一个指向 IRP 的指针，以便设置或检索\_条件\_ACCEPT socket 选项的状态。

此套接字选项的默认状态是禁用条件接受模式。

某些传输协议可能不支持侦听套接字上的条件接受模式。

有关有条件地接受传入连接的详细信息，请参阅[侦听和接受传入连接](https://docs.microsoft.com/windows-hardware/drivers/network/listening-for-and-accepting-incoming-connections)。

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

 

 




