---
title: SO_EXCLUSIVEADDRUSE
description: SO_EXCLUSIVEADDRUSE
ms.assetid: d281086f-4d8b-4e1e-b2bd-7b0a20338222
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_EXCLUSIVEADDRUSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 487a9c2557341cfb7eba1b6fddc414ccf3b0677c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376411"
---
# <a name="soexclusiveaddruse"></a>因此\_EXCLUSIVEADDRUSE


SO 的状态\_EXCLUSIVEADDRUSE 套接字选项用于确定是否将向其绑定套接字的本地传输地址以独占方式保留以供该套接字。 此套接字选项仅适用于侦听套接字、 数据报套接字和面向连接的套接字。

如果 WSK 应用程序将此套接字选项，则它必须实现之前接字绑定到本地传输地址。

若要设置此套接字选项的状态，WSK 应用程序调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)使用以下参数的函数。

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
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
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
<p>0:禁用独占使用的本地传输地址</p>
<p>1：启用独占使用的本地传输地址</p></td>
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
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
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
<p>0:禁用了独占使用的本地传输地址</p>
<p>1：启用独占使用的本地传输地址</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK 应用程序调用时必须指定一个指向 IRP **WskControlSocket**函数来设置或检索的状态等\_EXCLUSIVEADDRUSE 套接字选项。

此套接字选项的默认状态是禁用了独占使用的本地传输地址。

详细了解使用 SO\_EXCLUSIVEADDRUSE 套接字选项和其影响上共享本地传输地址之间套接字，请参阅[共享传输地址](https://docs.microsoft.com/windows-hardware/drivers/network/sharing-transport-addresses)。

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

 

 




