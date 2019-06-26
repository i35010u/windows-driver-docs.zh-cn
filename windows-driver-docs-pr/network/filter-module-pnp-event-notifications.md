---
title: 筛选器模块 PnP 事件通知
description: 筛选器模块 PnP 事件通知
ms.assetid: ca1e250a-aaa8-4fbc-abe5-c30c8913a67a
keywords:
- 筛选器模块 WDK 网络中，PnP 事件通知
- 筛选器驱动程序 WDK 网络中，PnP 事件通知
- NDIS 筛选器驱动程序 WDK，事件通知
- 事件通知 WDK 网络筛选器驱动程序
- 插 WDK 网络、 筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dacf5af6377f848e11cd584f43582fc83f2b33ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363415"
---
# <a name="filter-module-pnp-event-notifications"></a>筛选器模块 PnP 事件通知





筛选器驱动程序可以接收的所有设备插 (PnP) 通知的基础的微型端口驱动程序都接收。 此外，筛选器驱动程序可以接收的所有网络即插即用通知的基础协议驱动程序都接收。即插即用通知的处理是特定的驱动程序。

下图说明了已筛选的设备即插即用事件通知。

![说明已筛选的设备插事件通知的关系图](images/pnpeventfilter.png)

筛选器驱动程序提供[ *FilterDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_device_pnp_event_notify) NDIS 调用以传递设备即插即用和电源管理事件通知中的函数。 它类似于[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)函数。

筛选器驱动程序可以将转发到基础驱动程序的设备即插即用和电源管理的事件。 若要将转发设备即插即用或电源管理事件，调用[ **NdisFDevicePnPEventNotify** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfdevicepnpeventnotify)函数。

下图说明了筛选的网络即插即用事件通知。

![说明筛选的网络设备插事件通知的关系图](images/netpnpeventfilter.png)

筛选器驱动程序提供[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event) NDIS 传入网络 PnP 和电源管理事件通知而调用的函数。 它类似于[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数。

筛选器驱动程序可以将转发到过量驱动程序的网络 PnP 和电源管理的事件。 若要将转发网络即插即用或电源管理事件，调用[ **NdisFNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfnetpnpevent)函数。

筛选器驱动程序应处理驱动程序堆栈的更改。 有关驱动程序堆栈更改的详细信息，请参阅[修改运行驱动程序堆栈](modifying-a-running-driver-stack.md)。

如有必要允许处理这些事件，NDIS 可以启动暂停操作后即插即用或电源管理通知。 有关详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

 

 





