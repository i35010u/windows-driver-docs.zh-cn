---
title: 暂停绑定
description: 暂停绑定
ms.assetid: 7f693904-d995-4fcb-8b88-9343a567602e
keywords:
- 协议驱动程序 WDK 网络绑定暂停
- NDIS 协议驱动程序 WDK，绑定暂停
- 绑定暂停 WDK 网络
- 绑定状态 WDK 网络
- 暂停绑定协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30bb08d8983f9bc3dc9a03c0f5ef27be204d684e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357595"
---
# <a name="pausing-a-binding"></a>暂停绑定





NDIS 发送协议驱动程序后网络 Plug and Play (PnP) 暂停的绑定的事件通知，该绑定将进入暂停状态。

若要通知的即插即用暂停事件，NDIS 调用协议驱动程序[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数与**NetEvent**隶属[ **NET\_PNP\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)结构设置为**NetEventPause**。 **缓冲区**成员包含[ **NDIS\_协议\_暂停\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_pause_parameters)结构。

在暂停状态下，协议驱动程序的绑定：

-   应启动任何新的发送请求。

-   必须等待未完成发送请求来完成。 NDIS 调用才会完成暂停操作[ **ProtocolSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数的驱动程序的所有未完成发送请求。

-   句柄应像往常一样接收的指示。 基础的微型端口驱动程序等待未完成接收要暂停操作完成之前返回的数据。 这可确保没有正在进行中的驱动程序堆栈接收操作后暂停微型端口驱动程序。

-   返回新应立即接收到 NDIS 的迹象。 如果有必要，驱动程序可以将复制此类之前将它们返回收到的指示。

有关协议驱动程序详细信息将发送和接收操作，请参阅[协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

绑定协议驱动程序完成后将进入暂停状态返回未完成接收指示绑定和 NDIS 已完成所有未完成发送请求的绑定。

在已暂停状态下，协议驱动程序的绑定：

-   不能做出任何发送请求。

-   返回应立即收到指示。 如果有必要，驱动程序可以将复制此类之前将它们返回收到的指示。

 

 





