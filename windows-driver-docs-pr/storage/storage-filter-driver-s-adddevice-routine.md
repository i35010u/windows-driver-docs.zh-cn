---
title: 存储筛选器驱动程序的 AddDevice 例程
description: 存储筛选器驱动程序的 AddDevice 例程
keywords:
- 存储筛选器驱动程序 WDK，AddDevice
- 筛选器驱动程序 WDK 存储，AddDevice
- SFD WDK 存储，AddDevice
- AddDevice 例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74f62e204ca1d70cb19fc610a2c245070ef4b1a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799299"
---
# <a name="storage-filter-drivers-adddevice-routine"></a>存储筛选器驱动程序的 AddDevice 例程

PnP 管理器会在检测到由该驱动程序控制的设备时调用存储筛选器驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。 存储筛选器驱动程序的 *AddDevice* 例程 (SFD) 与存储类驱动程序的相同，不同之处在于，它不能尝试声明设备 (SRB_FUNCTION_CLAIM_DEVICE) 。

有关存储类驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程的信息，请参阅 [存储类驱动程序](introduction-to-storage-class-drivers.md)。 有关 PnP 驱动程序的 *AddDevice* 例程的一般信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)。
