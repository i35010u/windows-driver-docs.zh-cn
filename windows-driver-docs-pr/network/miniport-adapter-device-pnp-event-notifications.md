---
title: 微型端口适配器设备 PnP 事件通知
description: 微型端口适配器设备 PnP 事件通知
ms.assetid: b9417d5d-1f99-480e-8021-e5dd02f28c36
keywords:
- 插 WDK 网络，处理即插即用事件通知
- 微型端口适配器 WDK 网络，插事件通知
- 适配器 WDK 网络，插事件通知
- MiniportDevicePnPEventNotify
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e55b2190c45a3c91d40ee39eb171fed9b6d68b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373971"
---
# <a name="miniport-adapter-device-pnp-event-notifications"></a>微型端口适配器设备 PnP 事件通知





NDIS 调用微型端口驱动程序[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)函数，以通知插即用 (PnP) 事件的驱动程序。

NDIS 提供了描述的即插即用事件的事件代码。 代码可以表示适配器已意外删除从系统或主机系统的电源配置文件已更改。

如果事件代码指示电源配置文件已更改，NDIS 还指示的更改的类型。 在系统电池电源运行，或者系统正在 AC 电源。

微型端口驱动程序应调整的适配器设置相应地。

 

 





