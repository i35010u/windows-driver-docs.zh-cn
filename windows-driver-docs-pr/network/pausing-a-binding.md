---
title: 暂停绑定
description: 暂停绑定
ms.assetid: 7f693904-d995-4fcb-8b88-9343a567602e
keywords:
- 协议驱动程序 WDK 网络，绑定暂停
- NDIS 协议驱动程序 WDK，绑定暂停
- 绑定暂停 WDK 网络
- 绑定状态 WDK 网络
- 暂停协议驱动程序绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4207de32cd07a9cc9dea5978cddb4ffc7e88b210
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212107"
---
# <a name="pausing-a-binding"></a>暂停绑定





在 NDIS 发送协议驱动程序后即插即用 (PnP) 暂停事件通知以进行绑定，该绑定将进入暂停状态。

为了通知 PnP 暂停事件的协议驱动程序，NDIS 将调用[*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数，并将[**NET \_ PnP \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构的**NetEvent**成员设置为**NetEventPause**。 该 **缓冲区** 成员包含 [**NDIS \_ 协议 \_ PAUSE \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_pause_parameters) 结构。

对于处于暂停状态的绑定，协议驱动程序：

-   不应启动任何新的发送请求。

-   必须等待完成的发送请求完成。 在 NDIS 为驱动程序的所有未完成发送请求调用 [**ProtocolSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete) 函数之前，暂停操作不会完成。

-   应照常处理接收指示。 基础微型端口驱动程序等待未完成的接收数据在完成暂停操作之前返回。 这可确保在小型端口驱动程序暂停后，驱动程序堆栈中不存在任何正在进行的接收操作。

-   应立即将新的接收指示返回到 NDIS。 如有必要，驱动程序可以在返回之前复制此类接收指示。

有关协议驱动程序发送和接收操作的详细信息，请参阅 [协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

当协议驱动程序为绑定返回了未完成的接收指示并且 NDIS 完成了绑定的所有未完成的发送请求后，绑定将进入暂停状态。

对于处于暂停状态的绑定，协议驱动程序：

-   不能进行任何发送请求。

-   应立即返回接收指示。 如有必要，驱动程序可以在返回之前复制此类接收指示。

 

