---
title: WSK_CACHE_SD
description: WSK_CACHE_SD
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_CACHE_SD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a6d81c687bc88c511738c5d4da23b95b91fd4bef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813625"
---
# <a name="wsk_cache_sd"></a>WSK \_ 缓存 \_ SD


WSK 应用程序使用 WSK \_ CACHE \_ SD client control 操作来获取可传递到 [**WskSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)、 [**WskSocketConnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)和 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数的安全描述符的缓存副本。

若要获取安全描述符的缓存副本，WSK 应用程序需要使用以下参数调用 [**WskControlClient**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_CACHE_SD</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (PSECURITY_DESCRIPTOR) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型化变量的指针。 此变量包含一个指向 SECURITY_DESCRIPTOR 结构的指针，该结构定义要缓存的未缓存的安全描述符。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (PSECURITY_DESCRIPTOR) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 PSECURITY_DESCRIPTOR 类型化变量的指针。 此变量接收指向描述缓存的安全描述符的 SECURITY_DESCRIPTOR 结构的指针。</p></td>
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

当不再需要安全描述符时，WSK 应用程序必须通过使用 [**WSK \_ release \_ SD**](wsk-release-sd.md) client control 操作来释放安全描述符的缓存副本。

有关安全描述符结构的详细信息 \_ ，请参阅 \_ Microsoft Windows SDK 文档中的安全描述符的参考页。

此客户端控制操作的 *Irp* 参数必须为 **NULL** 。

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
<td>Wsk (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

