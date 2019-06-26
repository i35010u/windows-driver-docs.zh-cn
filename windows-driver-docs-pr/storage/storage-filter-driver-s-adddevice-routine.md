---
title: 存储筛选器驱动程序的 AddDevice 例程
description: 存储筛选器驱动程序的 AddDevice 例程
ms.assetid: 7970fb3e-4e4c-4ff7-9738-e09454a864c4
keywords:
- 存储筛选器驱动程序 WDK AddDevice
- 筛选器驱动程序 WDK 存储 AddDevice
- SFD WDK 存储 AddDevice
- AddDevice 例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 244e6799c4177f13a121257becbc2908ca1e506a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368206"
---
# <a name="storage-filter-drivers-adddevice-routine"></a>存储筛选器驱动程序的 AddDevice 例程


## <span id="ddk_storage_filter_driver_s_adddevice_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_ADDDEVICE_ROUTINE_KG"></span>


PnP 管理器调用[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)存储筛选器驱动程序检测到由该驱动程序控制的设备时的例程。 *AddDevice*例程存储筛选器驱动程序 (SFD) 是类似的存储类驱动程序，不同之处在于它不能尝试声明设备 (SRB\_函数\_声明\_设备)。

有关存储类驱动程序的信息[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程，请参阅[存储类驱动程序](storage-class-drivers.md)。 有关即插即用驱动程序的常规信息*AddDevice*例程，请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

 




