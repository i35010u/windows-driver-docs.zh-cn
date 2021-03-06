---
title: 重启绑定
description: 重启绑定
keywords:
- 协议驱动程序 WDK 网络，绑定重新启动
- NDIS 协议驱动程序 WDK，绑定重新启动
- 绑定重新启动 WDK 网络
- 绑定状态 WDK 网络
- 正在重新启动协议驱动程序绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d083d792791b8ec3450cc280a99aef8a731ed9c9
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248975"
---
# <a name="restarting-a-binding"></a>重启绑定





为了重新启动已暂停的绑定，NDIS 会将协议驱动程序即插即用 (PnP) restart 事件通知发送到一个网络。 协议驱动程序收到重新启动通知后，受影响的绑定将进入重新启动状态。

为了发送重新启动通知，NDIS 调用了协议驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 NDIS 传递到 *ProtocolNetPnPEvent* 的 [**NET \_ PNP \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构在 **NetEvent** 成员中指定 **NetEventRestart** ，而 **缓冲区** 成员包含指向 [**NDIS \_ 协议 \_ RESTART \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_restart_parameters)结构的指针。 NDIS 在 NDIS 协议重新启动参数结构的 RestartAttributes 成员中提供了指向 [**ndis \_ RESTART \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)结构的指针 \_ \_ \_ 。

**注意**  绑定暂停时，NDIS 可能已重新配置了驱动程序堆栈。 新的堆栈配置可以支持基础适配器的不同功能集。 这些新功能可能会影响协议驱动程序在绑定上的通信方式。

 

协议驱动程序应使用 [**NDIS \_ 协议 \_ 重新启动 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_restart_parameters) 结构中的信息，以避免不必要的 OID 请求。

在重新启动状态下，协议驱动程序可以：

-   使用 OID 请求查询驱动程序堆栈。 例如，驱动程序可以通过使用 [OID 生成 \_ \_ 接收 \_ 缩放 \_ 功能](./oid-gen-receive-scale-capabilities.md)来了解对接收方缩放的支持。

-   如有必要，重新分配 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 和 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 池。

-   枚举基础筛选器模块的列表。

-   使用 OID 请求来显示新的适配器功能。

当驱动程序准备好恢复绑定的发送和接收操作后，绑定将进入 "正在运行" 状态。

 

