---
title: 微型端口适配器设备 PnP 事件通知
description: 微型端口适配器设备 PnP 事件通知
ms.assetid: b9417d5d-1f99-480e-8021-e5dd02f28c36
keywords:
- 即插即用 WDK 网络，处理 PnP 事件通知
- 微型端口适配器 WDK 网络，即插即用事件通知
- 适配器 WDK 网络，即插即用事件通知
- MiniportDevicePnPEventNotify
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8a9dda1cd5069dc5cbbd6b83df613dca753bbf2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844255"
---
# <a name="miniport-adapter-device-pnp-event-notifications"></a>微型端口适配器设备 PnP 事件通知





NDIS 调用微型端口驱动程序的[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)函数，将即插即用（PnP）事件的驱动程序通知给驱动程序。

NDIS 提供了一个描述 PnP 事件的事件代码。 此代码可能表示适配器已从系统中意外删除，或者主机系统的电源配置文件已更改。

如果事件代码指示电源配置文件已更改，NDIS 还会指示更改的类型。 系统正在使用电池电源运行，或者系统正在通过交流电源运行。

微型端口驱动程序应该相应地调整适配器设置。

 

 





