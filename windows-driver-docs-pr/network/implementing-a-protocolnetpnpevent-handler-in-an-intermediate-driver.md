---
title: 实现中间驱动程序 ProtocolNetPnPEvent 处理程序
description: 在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序
ms.assetid: 1d0475c4-631d-4b8a-ab26-5b8b9425bfe6
keywords:
- ProtocolNetPnPEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82bf35f94c0eb76d7e8ee080c106ba769a13944b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843399"
---
# <a name="implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver"></a>在中间驱动程序中实现 ProtocolNetPnPEvent 处理程序





中间驱动程序中[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数的实现与协议驱动程序中的实现几乎完全相同。 有关在中间驱动程序中实现*ProtocolNetPnPEvent*处理程序的详细信息，请参阅[在协议驱动程序中处理 PNP 事件和 PM 事件](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)。

NDIS 中间驱动程序通过调用[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数将 PnP 事件传递到更高层的驱动程序。

 

 





