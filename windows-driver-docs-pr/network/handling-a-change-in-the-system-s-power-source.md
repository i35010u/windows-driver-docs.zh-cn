---
title: 处理系统电源的更改
description: 处理系统电源的更改
keywords:
- power source 更改 WDK 网络
- Nic WDK 网络，电源更改
- 网络接口卡 WDK 网络，电源更改
- 即插即用 WDK NDIS 微型端口，电源更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0e0da018110d6e33a09291b907864bb26fd2fc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840017"
---
# <a name="handling-a-change-in-the-systems-power-source"></a>处理系统电源的更改





系统可以从电池电源切换到 AC 电源，反之亦然。

初始化微型端口驱动程序之后，NDIS 会调用微型端口驱动程序的 [*MiniportDevicePnPEventNotify*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify) 函数，以通知系统电源的微型端口驱动程序。 微型端口驱动程序可以使用此信息调整 NIC 的功率消耗。 例如，如果系统正在使用电池电源运行，则无线 LAN 的微型端口驱动程序 (WLAN) 设备可能会降低功耗，或在系统使用 AC 电源运行时增加功率消耗。

 

