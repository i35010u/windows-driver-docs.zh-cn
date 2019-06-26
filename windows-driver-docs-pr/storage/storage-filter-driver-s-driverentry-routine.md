---
title: 存储筛选器驱动程序的 DriverEntry 例程
description: 存储筛选器驱动程序的 DriverEntry 例程
ms.assetid: 801daf42-259d-45ab-a5c5-88acb2d35bef
keywords:
- 存储筛选器驱动程序 WDK DriverEntry
- 筛选器驱动程序 WDK 存储 DriverEntry
- SFD WDK 存储 DriverEntry
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 524b38474d6790acff446706465183a43e0353e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376687"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>存储筛选器驱动程序的 DriverEntry 例程


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


像任何其他内核模式驱动程序， [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)存储筛选器驱动程序 (SFD) 的例程必须输入驱动程序对象中定义其调度和其他入口点。 如果有必要，SFD 可以分配一个驱动程序的适当大小的对象扩展通过调用[ **IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatedriverobjectextension)，将输入的注册表路径复制到更高版本使用的驱动程序扩展和如果有，请初始化与其他驱动程序确定的数据，该驱动程序扩展。

有关即插即用驱动程序的详细信息[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程，请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

 




