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
ms.openlocfilehash: 6287beab71ccb1808d1a48b8eb4cae5702bb7908
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188793"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>存储筛选器驱动程序的 DriverEntry 例程


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


与任何其他内核模式驱动程序一样，存储筛选器驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程 (SFD) 必须在输入驱动程序对象中定义其调度和其他入口点。 如有必要，SFD 可以通过调用 [**IoAllocateDriverObjectExtension**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)分配适当大小的驱动程序对象扩展，将输入注册表路径复制到驱动程序扩展以供将来使用，并使用其他驱动程序确定的数据初始化驱动程序扩展（如果有）。

有关 PnP 驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程的详细信息，请参阅 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

