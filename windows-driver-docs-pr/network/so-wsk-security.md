---
title: SO_WSK_SECURITY
description: SO_WSK_SECURITY
ms.assetid: 169680ba-6486-48fe-89d7-dcd4e5930605
ms.date: 07/18/2017
keywords:
- SO_WSK_SECURITY 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ff1f423294f6c296c6b984b203640c860fdcb889
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841877"
---
# <a name="so_wsk_security"></a>\_WSK\_安全性


SO\_WSK\_SECURITY socket 选项允许 WSK 应用程序将安全描述符应用到套接字，或从套接字检索套接字安全描述符的缓存副本。 安全描述符控制套接字绑定到的本地传输地址的共享。

此套接字选项仅适用于侦听套接字、数据报套接字和面向连接的套接字。

如果 WSK 应用程序使用此套接字选项来将安全描述符应用于套接字，则必须在将套接字绑定到本地传输地址之前执行此操作。

若要将安全描述符应用于套接字，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p>SO_WSK_SECURITY</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （PSECURITY_DESCRIPTOR）</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量必须包含指向安全描述符缓存副本的指针，该安全描述符是通过使用<a href="wsk-cache-sd.md" data-raw-source="[&lt;strong&gt;WSK_CACHE_SD&lt;/strong&gt;](wsk-cache-sd.md)"><strong>WSK_CACHE_SD</strong></a>控制代码调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client" data-raw-source="[&lt;strong&gt;WskControlClient&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)"><strong>WskControlClient</strong></a>函数获取的。</p></td>
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

调用**WskControlSocket**函数以将安全描述符应用于套接字时，WSK 应用程序必须指定一个指向 IRP 的指针。

如果 WSK 应用程序使用此套接字选项将安全描述符应用于套接字，则新的安全描述符将替换以前应用于套接字的任何安全描述符。

在完成 IRP 后，WSK 应用程序不能释放安全描述符的缓存副本。

WSK 应用程序还可以在套接字最初创建时，通过在*SecurityDescriptor*参数中指定指向安全描述符缓存副本的指针（在调用[**WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)或[**WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)函数。

如果 WSK 应用程序不会将安全描述符应用于套接字，则 WSK 子系统将使用不允许共享本地传输地址的默认安全描述符。

若要从套接字检索套接字安全描述符的缓存副本，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p>SO_WSK_SECURITY</p></td>
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
<td><p>sizeof （PSECURITY_DESCRIPTOR）</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量接收指向套接字安全描述符的缓存副本的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

在调用**WskControlSocket**函数从套接字检索套接字安全描述符的缓存副本时，WSK 应用程序必须指定一个指向 IRP 的指针。

WSK 应用程序必须使用[**WSK\_release\_SD**](wsk-release-sd.md)控制代码调用[**WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)函数，以便在不再需要安全描述符的缓存副本时将其释放。

有关安全\_描述符结构的详细信息，请参阅 Microsoft Windows SDK 文档中的安全性\_描述符的参考页。

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

 

 




