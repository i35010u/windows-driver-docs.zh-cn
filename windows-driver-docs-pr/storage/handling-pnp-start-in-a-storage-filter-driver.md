---
title: 处理存储筛选器驱动程序中的 PnP 启动
description: 处理存储筛选器驱动程序中的 PnP 启动
ms.assetid: 02a87fec-772d-4416-bd3a-5c7f98e8d55e
keywords:
- 存储筛选器驱动程序 WDK、PnP
- 筛选器驱动程序 WDK 存储，PnP
- SFD WDK 存储，PnP
- PnP WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f21e1473326d24647bfce864683b94600648eba
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606517"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>处理存储筛选器驱动程序中的 PnP 启动

存储筛选器驱动程序（SFD）执行特定于设备的初始化，并在 PnP 管理器使用启动请求（[**irp\_MJ\_pnp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp) ，并使用[**irp\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)）[*调用其设备*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)扩展。 SFD 处理启动请求的方式与存储类驱动程序的处理方式几乎相同。

有关存储类驱动程序如何处理启动请求并设置其设备扩展的信息，请参阅[存储类驱动程序](introduction-to-storage-class-drivers.md)。 有关处理 PnP 开始请求的常规信息，请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。
