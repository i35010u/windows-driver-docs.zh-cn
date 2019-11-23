---
title: 重启绑定
description: 重启绑定
ms.assetid: 5abec927-cb73-4b02-b977-c4f45bd37c42
keywords:
- 协议驱动程序 WDK 网络，绑定重新启动
- NDIS 协议驱动程序 WDK，绑定重新启动
- 绑定重新启动 WDK 网络
- 绑定状态 WDK 网络
- 正在重新启动协议驱动程序绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0edc77afea74d696c0fe4c03593d585125badd8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842017"
---
# <a name="restarting-a-binding"></a>重启绑定





为了重新启动已暂停的绑定，NDIS 将向协议驱动程序发送网络即插即用（PnP）重新启动事件通知。 协议驱动程序收到重新启动通知后，受影响的绑定将进入重新启动状态。

为了发送重新启动通知，NDIS 调用了协议驱动程序的[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。 \_NDIS 传递到*ProtocolNetPnPEvent*的[**NET\_PNP 事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构在**NetEvent**成员中指定了**NetEventRestart** ，而该**缓冲区**成员包含指向[**NDIS\_协议的指针\_RESTART\_的参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_restart_parameters)结构。 NDIS 提供指向 Ndis 的指针[ **\_重启**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)NDIS\_协议的**RestartAttributes**成员中\_属性结构\_重启\_参数结构。

**请注意**  绑定暂停时，NDIS 可能已重新配置驱动程序堆栈。 新的堆栈配置可以支持基础适配器的不同功能集。 这些新功能可能会影响协议驱动程序在绑定上的通信方式。

 

协议驱动程序应使用[**NDIS\_协议中的信息\_RESTART\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_restart_parameters)结构，以避免不必要的 OID 请求。

在重新启动状态下，协议驱动程序可以：

-   使用 OID 请求查询驱动程序堆栈。 例如，驱动程序可以通过使用[OID\_GEN\_接收\_扩展\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-capabilities)，来找出对接收方缩放的支持。

-   如有必要，重新分配[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)和[**net\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)池。

-   枚举基础筛选器模块的列表。

-   使用 OID 请求来显示新的适配器功能。

当驱动程序准备好恢复绑定的发送和接收操作后，绑定将进入 "正在运行" 状态。

 

 





