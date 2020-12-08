---
title: 处理存储筛选器驱动程序中的 PnP 启动
description: 处理存储筛选器驱动程序中的 PnP 启动
keywords:
- 存储筛选器驱动程序 WDK、PnP
- 筛选器驱动程序 WDK 存储，PnP
- SFD WDK 存储，PnP
- PnP WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e2447d24a6bd3ed53f46067ea025b8edf83b833
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835221"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>处理存储筛选器驱动程序中的 PnP 启动

存储筛选器驱动程序 (SFD) 执行特定于设备的初始化，并在 PnP 管理器使用启动请求调用其 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程 ([**irp \_ MJ \_ PnP**](../kernel/irp-mj-pnp.md) with [**irp \_ MN \_ start \_ device**](../kernel/irp-mn-start-device.md)) 时设置其设备扩展。 SFD 处理启动请求的方式与存储类驱动程序的处理方式几乎相同。

有关存储类驱动程序如何处理启动请求并设置其设备扩展的信息，请参阅 [存储类驱动程序](introduction-to-storage-class-drivers.md)。 有关处理 PnP 开始请求的常规信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)。
