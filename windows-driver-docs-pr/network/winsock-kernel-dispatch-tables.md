---
title: Winsock 内核调度表
description: Winsock 内核调度表
ms.assetid: 391c6868-fb85-41ea-ada5-6ba90750300c
keywords:
- Winsock 内核 WDK 网络，调度表
- WSK WDK 网络，调度表
- 调度表 WDK Winsock 内核
- 函数 WDK Winsock 内核
- 基本套接字 WDK Winsock 内核
- 侦听套接字 WDK Winsock 内核
- 数据报套接字 WDK Winsock 内核
- 面向连接的套接字 WDK Winsock 内核
- 事件回调函数 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8497b00cd2f6e330777107b84246a19959a9e8e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107202"
---
# <a name="winsock-kernel-dispatch-tables"></a>Winsock 内核调度表


Winsock 内核 (WSK) 套接字的 [套接字对象](winsock-kernel-objects.md) 包含指向提供程序调度表结构的指针，该结构包含指向套接字支持的套接字函数的函数指针。 WSK 应用程序调用提供程序调度表结构中的函数来执行套接字上的网络 i/o 操作。 由于每个 WSK [套接字类别](winsock-kernel-socket-categories.md) 都支持一组不同的套接字函数，WSK [网络编程接口 (NPI) ](network-programming-interface.md) 为每个类别的 WSK 套接字定义不同的提供程序调度表结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">套接字类别</th>
<th align="left">调度表结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>基本套接字</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_basic_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_BASIC_DISPATCH&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_basic_dispatch)"><strong>WSK_PROVIDER_BASIC_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>侦听套接字</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_listen_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_LISTEN_DISPATCH&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_listen_dispatch)"><strong>WSK_PROVIDER_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据报套接字</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_datagram_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_DATAGRAM_DISPATCH&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_datagram_dispatch)"><strong>WSK_PROVIDER_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>面向连接的套接字</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_connection_dispatch" data-raw-source="[&lt;strong&gt;WSK_PROVIDER_CONNECTION_DISPATCH&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_connection_dispatch)"><strong>WSK_PROVIDER_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

如果 WSK 应用程序对其创建的套接字使用事件回调函数，则在创建新的套接字时，它必须提供包含指向套接字事件回调函数的函数指针的客户端调度表结构。 由于每个 WSK 套接字类别都支持一组不同的事件回调函数，因此 WSK NPI 为每个 WSK 套接字类别定义了不同的客户端调度表结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">套接字类别</th>
<th align="left">调度表结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>侦听套接字</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_listen_dispatch" data-raw-source="[&lt;strong&gt;WSK_CLIENT_LISTEN_DISPATCH&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_listen_dispatch)"><strong>WSK_CLIENT_LISTEN_DISPATCH</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>数据报套接字</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_datagram_dispatch" data-raw-source="[&lt;strong&gt;WSK_CLIENT_DATAGRAM_DISPATCH&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_datagram_dispatch)"><strong>WSK_CLIENT_DATAGRAM_DISPATCH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>面向连接的套接字</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_connection_dispatch" data-raw-source="[&lt;strong&gt;WSK_CLIENT_CONNECTION_DISPATCH&lt;/strong&gt;](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_connection_dispatch)"><strong>WSK_CLIENT_CONNECTION_DISPATCH</strong></a></p></td>
</tr>
</tbody>
</table>

 

**注意**   基本套接字不支持任何事件回调函数。 因此，不会为基本套接字定义任何客户端调度表结构。

 

