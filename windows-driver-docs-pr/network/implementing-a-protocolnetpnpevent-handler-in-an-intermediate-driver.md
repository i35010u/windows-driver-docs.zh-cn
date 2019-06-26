---
title: 实现一个中间驱动程序 ProtocolNetPnPEvent 处理程序
description: 在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序
ms.assetid: 1d0475c4-631d-4b8a-ab26-5b8b9425bfe6
keywords:
- ProtocolNetPnPEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 283b273bc2af1f365cbfe374bd93ea0443e897e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382696"
---
# <a name="implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver"></a>在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序





实现[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)中间驱动程序中的函数是协议驱动程序中实现几乎完全相同。 有关实现详细信息*ProtocolNetPnPEvent*处理程序中的中间驱动程序，请参阅[处理即插即用事件和协议驱动程序中的 PM 事件](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)。

NDIS 中间的驱动程序通过即插即用事件到更高的层驱动程序通过调用[ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)函数。

 

 





