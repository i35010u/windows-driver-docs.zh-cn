---
title: 存储筛选器驱动程序的 AddDevice 例程
description: 存储筛选器驱动程序的 AddDevice 例程
ms.assetid: 7970fb3e-4e4c-4ff7-9738-e09454a864c4
keywords:
- 存储筛选器驱动程序 WDK，AddDevice
- 筛选器驱动程序 WDK 存储，AddDevice
- SFD WDK 存储，AddDevice
- AddDevice 例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f546dfe38c6672f083206c3fa0c3417a9dfa17a
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733706"
---
# <a name="storage-filter-drivers-adddevice-routine"></a>存储筛选器驱动程序的 AddDevice 例程

PnP 管理器会在检测到由该驱动程序控制的设备时调用存储筛选器驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。 存储筛选器驱动程序的 *AddDevice* 例程 (SFD) 与存储类驱动程序的相同，不同之处在于，它不能尝试声明设备 (SRB_FUNCTION_CLAIM_DEVICE) 。

有关存储类驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程的信息，请参阅 [存储类驱动程序](introduction-to-storage-class-drivers.md)。 有关 PnP 驱动程序的 *AddDevice* 例程的一般信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)。