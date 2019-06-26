---
title: WSK_CACHE_SD
description: WSK_CACHE_SD
ms.assetid: 60a4c7f9-d7e3-4378-b22b-93c69a9b8a37
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_CACHE_SD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d60a21a8e85b32aecd935af1d5c573246acc8d32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377943"
---
# <a name="wskcachesd"></a>WSK\_CACHE\_SD


WSK 应用程序使用 WSK\_缓存\_SD 客户端控制操作，以获取可以传递到的安全描述符的缓存的副本[ **WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)， [ **WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)，并[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)函数。

若要获取的安全描述符的缓存的副本，WSK 应用程序调用[ **WskControlClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client)使用以下参数的函数。

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
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_CACHE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量包含指向定义正在缓存的未缓存的安全描述符的 SECURITY_DESCRIPTOR 结构的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(PSECURITY_DESCRIPTOR)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型的变量的指针。 此变量接收指向描述的缓存的安全描述符的 SECURITY_DESCRIPTOR 结构的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Irp</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

WSK 应用程序必须通过使用发布的安全描述符的缓存的副本[ **WSK\_发行\_SD** ](wsk-release-sd.md)客户端管理操作的安全描述符时没有不再需要。

有关安全性的详细信息\_描述符结构，请参阅有关安全的参考页\_Microsoft Windows SDK 文档中的描述符。

*Irp*参数必须是**NULL**此客户端控制操作。

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

 

 




