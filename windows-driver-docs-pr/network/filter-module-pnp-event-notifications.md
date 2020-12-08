---
title: 筛选器模块 PnP 事件通知
description: 筛选器模块 PnP 事件通知
keywords:
- 筛选器模块 WDK 网络，PnP 事件通知
- 筛选器驱动程序 WDK 网络，PnP 事件通知
- NDIS 筛选器驱动程序 WDK，事件通知
- 事件通知 WDK 网络，筛选器驱动程序
- 即插即用 WDK 网络，筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e53deb525ca94442e481e0759eac42096843d846
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808073"
---
# <a name="filter-module-pnp-event-notifications"></a>筛选器模块 PnP 事件通知





筛选器驱动程序可以接收基础微型端口驱动程序接收即插即用 (PnP) 通知的所有设备。 此外，筛选器驱动程序还可以接收过量协议驱动程序接收的所有网络 PnP 通知。PnP 通知的处理特定于驱动程序。

下图说明了已筛选设备 PnP 事件通知。

![说明已筛选设备即插即用事件通知的示意图](images/pnpeventfilter.png)

筛选器驱动程序提供了一个 [*FilterDevicePnPEventNotify*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_device_pnp_event_notify) 函数，该函数可通过 NDIS 调用来传入设备 PnP 和电源管理事件通知。 这类似于 [*MiniportDevicePnPEventNotify*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify) 函数。

筛选器驱动程序可以将设备 PnP 和电源管理事件转发到底层驱动程序。 若要转发设备 PnP 或电源管理事件，请调用 [**NdisFDevicePnPEventNotify**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfdevicepnpeventnotify) 函数。

下图说明了筛选的网络 PnP 事件通知。

![说明已筛选网络设备即插即用事件通知的示意图](images/netpnpeventfilter.png)

筛选器驱动程序提供了一个 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数，该函数可通过 NDIS 调用来传入网络 PnP 和电源管理事件通知。 这类似于 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。

筛选器驱动程序可以将网络 PnP 和电源管理事件转发到过量驱动程序。 若要转发网络 PnP 或电源管理事件，请调用 [**NdisFNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) 函数。

筛选器驱动程序应处理驱动程序堆栈更改。 有关驱动程序堆栈更改的详细信息，请参阅 [修改正在运行的驱动程序堆栈](modifying-a-running-driver-stack.md)。

如有必要允许处理这些事件，NDIS 可以在 PnP 或电源管理通知之后启动暂停操作。 有关详细信息，请参阅 [暂停驱动程序堆栈](pausing-a-driver-stack.md)。

 

