---
title: 处理协议驱动程序中的 PnP 事件通知
description: 处理协议驱动程序中的 PnP 事件通知
ms.assetid: 7c6c9bc5-37ce-49f4-8e39-5f51a266836a
keywords:
- 即插即用 WDK NDIS 协议
- 通知 WDK 即插即用，协议的 NDIS 驱动程序
- 事件通知 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a68625b8caae2096233e9b5ff811568afba7a2f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379779"
---
# <a name="handling-pnp-event-notifications-in-a-protocol-driver"></a>处理协议驱动程序中的 PnP 事件通知





NDIS 6.0 和更高版本的协议驱动程序处理同一插即用 (PnP) 事件通知作为除了到 NDIS 6.0 及更高版本特定的事件通知的 NDIS 5.x 驱动程序。 即插即用事件通知的处理是特定的驱动程序。

若要通知网络即插即用事件协议驱动程序，NDIS 调用驱动程序的[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数。 若要定义的事件的事件类型和特征，NDIS 传递[ **NET\_PNP\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)结构在*NetPnPEvent*的事件参数*ProtocolNetPnPEvent*。

协议驱动程序应处理驱动程序堆栈的更改。 有关驱动程序堆栈更改的详细信息，请参阅[修改运行驱动程序堆栈](modifying-a-running-driver-stack.md)。

无法处理堆栈更改通知的协议驱动程序是适配器和重新绑定已解除。 不受影响的协议驱动程序已成功处理驱动程序堆栈通知绑定。

协议驱动程序应处理驱动程序堆栈暂停通知。 有关这些通知的详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

协议驱动程序应处理驱动程序堆栈重启通知。 有关这些通知的详细信息，请参阅[重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

 

 





