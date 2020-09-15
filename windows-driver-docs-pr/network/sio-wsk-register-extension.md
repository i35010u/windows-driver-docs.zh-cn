---
title: SIO_WSK_REGISTER_EXTENSION
description: SIO_WSK_REGISTER_EXTENSION
ms.assetid: e7fd6d68-85e8-4c5f-b67f-2193d200130d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_REGISTER_EXTENSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a4b0ad9b071926f93187fd49ce6e4b24b906a477
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102980"
---
# <a name="sio_wsk_register_extension"></a>SIO \_ WSK \_ 注册 \_ 扩展


SIO \_ WSK \_ register \_ EXTENSION socket i/o CONTROL 操作允许 WSK 应用程序注册 WSK 子系统支持的扩展接口。 此套接字 i/o 控制操作适用于所有套接字类型。

若要注册扩展接口，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_REGISTER_EXTENSION</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (WSK_EXTENSION_CONTROL_IN) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 <a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_in" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_IN&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_in)"><strong>WSK_EXTENSION_CONTROL_IN</strong></a> 结构的指针。 此结构包含一个指向网络编程接口的指针，该指针指向扩展接口 <a href="/windows-hardware/drivers/network/network-programming-interface" data-raw-source="[Network Programming Interface (NPI)](./network-programming-interface.md)"> (NPI) </a> 标识符，以及指向调度表的指针和指向该扩展接口的 WSK 应用程序实现上下文的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (WSK_EXTENSION_CONTROL_OUT) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 <a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_out" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_OUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_extension_control_out)"><strong>WSK_EXTENSION_CONTROL_OUT</strong></a> 结构的指针。 此结构接收指向调度表的指针和指向扩展接口的 WSK 子系统实现上下文的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>


调用 **WskControlSocket** 函数注册扩展接口时，WSK 应用程序不指定指向 IRP 的指针。

调度表结构的内容是扩展接口特定的。

有关注册扩展接口的详细信息，请参阅 [注册扩展接口](./registering-an-extension-interface.md)。

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

