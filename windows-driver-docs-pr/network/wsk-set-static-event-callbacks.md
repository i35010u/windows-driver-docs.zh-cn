---
title: WSK_SET_STATIC_EVENT_CALLBACKS
description: WSK_SET_STATIC_EVENT_CALLBACKS
ms.assetid: fa95bc7d-c7b2-4cca-a419-ef5eb2520976
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WSK_SET_STATIC_EVENT_CALLBACKS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d2df1acfdeaa843df2781bede4116fcd0567b654
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207741"
---
# <a name="wsk_set_static_event_callbacks"></a>WSK \_ 设置 \_ 静态 \_ 事件 \_ 回调


WSK 应用程序使用 WSK \_ 设置 \_ 静态 \_ 事件 \_ 回调客户端控制操作，在其创建的每个套接字上自动启用特定的事件回调函数。 以这种方式启用的事件回调函数始终处于启用状态，并且不能在以后由 WSK 应用程序禁用或重新启用。 但是，如果 WSK 应用程序始终在其创建的每个套接字上启用特定的事件回调函数，则应用程序应使用此方法来自动启用这些事件回调函数，因为它将产生更好的性能。

如果 WSK 应用程序使用 WSK \_ 设置 \_ 静态 \_ 事件 \_ 回调客户端控制操作，则必须在创建任何套接字之前执行此操作。

若要在它创建的每个套接字上自动启用特定的事件回调函数，WSK 应用程序需要使用以下参数调用 [**WskControlClient**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) 函数。

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
<td><p><em>ControlCode</em></p></td>
<td><p>WSK_SET_STATIC_EVENT_CALLBACKS</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (WSK_EVENT_CALLBACK_CONTROL) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control" data-raw-source="[&lt;strong&gt;WSK_EVENT_CALLBACK_CONTROL&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)"><strong>WSK_EVENT_CALLBACK_CONTROL</strong></a> 结构的指针，该结构指定要自动启用的所需事件回调函数</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
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

WSK 应用程序可以在[**WSK \_ 事件 \_ 回调 \_ 控制**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_event_callback_control)结构的**EventMask**成员中指定不同套接字类型的事件标志的组合。 当 WSK 应用程序创建新的套接字时，WSK 子系统将自动为正在创建的 WSK 套接字的特定 [类别](./winsock-kernel-socket-categories.md) 启用适当的事件回调函数。

有关标准 WSK 事件回调函数的事件标志的详细信息，请参阅 [** \_ WSK \_ 事件 \_ 回调**](so-wsk-event-callback.md)。

有关启用和禁用套接字的事件回调函数的详细信息，请参阅 [启用和禁用事件回调函数](./enabling-and-disabling-event-callback-functions.md)。

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

 

