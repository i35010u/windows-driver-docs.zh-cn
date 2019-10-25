---
title: 处理协议驱动程序中的 PnP 事件通知
description: 处理协议驱动程序中的 PnP 事件通知
ms.assetid: 7c6c9bc5-37ce-49f4-8e39-5f51a266836a
keywords:
- 即插即用 WDK NDIS 协议
- 通知 WDK PnP，NDIS 协议驱动程序
- 事件通知 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d11b7a42493cd60c13a0f3c0e7477634161fbab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842570"
---
# <a name="handling-pnp-event-notifications-in-a-protocol-driver"></a>处理协议驱动程序中的 PnP 事件通知





除了特定于 NDIS 6.0 和更高版本的事件通知外，NDIS 6.0 和更高版本的协议驱动程序还处理与 NDIS 1.x 驱动程序相同的即插即用（PnP）事件通知。 PnP 事件通知的处理特定于驱动程序。

为了通知网络 PnP 事件的协议驱动程序，NDIS 调用了驱动程序的[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。 为了定义事件类型和事件的特征，NDIS 在*ProtocolNetPnPEvent*的*NetPnPEvent*事件参数中传递了[**NET\_PNP\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构。

协议驱动程序应处理驱动程序堆栈更改。 有关驱动程序堆栈更改的详细信息，请参阅[修改正在运行的驱动程序堆栈](modifying-a-running-driver-stack.md)。

不处理堆栈更改通知的协议驱动程序将从适配器解除绑定，并重新绑定。 成功处理驱动程序堆栈通知的协议驱动程序的绑定不受影响。

协议驱动程序应处理驱动程序堆栈暂停通知。 有关这些通知的详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

协议驱动程序应处理驱动程序堆栈重新启动通知。 有关这些通知的详细信息，请参阅[重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

 

 





