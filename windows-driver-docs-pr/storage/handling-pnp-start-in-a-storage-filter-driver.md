---
title: 处理存储筛选器驱动程序中的 PnP 启动
description: 处理存储筛选器驱动程序中的 PnP 启动
ms.assetid: 02a87fec-772d-4416-bd3a-5c7f98e8d55e
keywords:
- 存储筛选器驱动程序 WDK，即插即用
- 筛选驱动程序 WDK 存储，即插即用
- SFD WDK 存储，即插即用
- 即插即用 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09933762e0eae8138ac1d9a894081e33fe459469
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378493"
---
# <a name="handling-pnp-start-in-a-storage-filter-driver"></a>处理存储筛选器驱动程序中的 PnP 启动


## <span id="ddk_handling_pnp_start_in_a_storage_filter_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_FILTER_DRIVER_KG"></span>


存储筛选器驱动程序 (SFD) 执行特定于设备的初始化并设置其设备扩展时即插即用管理器会调用其[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程替换一个开始请求 ([ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)与[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 存储类驱动程序一样，SFD 将处理在很大程度的开始请求相同的方式。

有关如何存储类驱动程序处理启动请求，并设置其设备扩展的信息，请参阅[存储类驱动程序](storage-class-drivers.md)。 有关处理即插即用启动请求的常规信息，请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

 




