---
title: 存储筛选器驱动程序的 DriverEntry 例程
description: 存储筛选器驱动程序的 DriverEntry 例程
ms.assetid: 801daf42-259d-45ab-a5c5-88acb2d35bef
keywords:
- 存储筛选器驱动程序 WDK，DriverEntry
- 筛选器驱动程序 WDK 存储，DriverEntry
- SFD WDK 存储，DriverEntry
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1263c1dee13b53a973d44f8d0caf36b77146149
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733613"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>存储筛选器驱动程序的 DriverEntry 例程


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


与任何其他内核模式驱动程序一样，存储筛选器驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程 (SFD) 必须在输入驱动程序对象中定义其调度和其他入口点。 如有必要，SFD 可以通过调用 [**IoAllocateDriverObjectExtension**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)分配适当大小的驱动程序对象扩展，将输入注册表路径复制到驱动程序扩展以供将来使用，并使用其他驱动程序确定的数据初始化驱动程序扩展（如果有）。

有关 PnP 驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程的详细信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)。

