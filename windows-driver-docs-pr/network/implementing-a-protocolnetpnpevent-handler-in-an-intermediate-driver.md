---
title: 实现中间驱动程序 ProtocolNetPnPEvent 处理程序
description: 在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序
keywords:
- ProtocolNetPnPEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab06e7a5f562f4ffc37469155b3ca3e7ebddef56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825087"
---
# <a name="implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver"></a>在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序





中间驱动程序中 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数的实现与协议驱动程序中的实现几乎完全相同。 有关在中间驱动程序中实现 *ProtocolNetPnPEvent* 处理程序的详细信息，请参阅 [在协议驱动程序中处理 PNP 事件和 PM 事件](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)。

NDIS 中间驱动程序通过调用 [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) 函数将 PnP 事件传递到更高层的驱动程序。

 

