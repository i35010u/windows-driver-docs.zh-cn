---
title: 处理对存储外设的 PnP 请求
description: 处理对存储外设的 PnP 请求
ms.assetid: 9c7ea576-11e6-46d7-b04c-ce412a0fc569
keywords:
- 外围设备 WDK 存储，即插即用请求
- 存储外围设备 WDK，即插即用请求
- 即插即用 WDK 存储
- 插 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 465717bdf58aa313528d117dc007fc72432ffb1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378501"
---
# <a name="handling-pnp-requests-to-storage-peripherals"></a>处理对存储外设的 PnP 请求


## <span id="ddk_handling_pnp_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_PNP_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


存储类驱动程序的*DispatchPnP*例程负责对即插即用请求的响应中的以下：

-   响应启动请求启动其设备 (IRP\_MJ\_IRP 与 PNP\_MN\_启动\_设备)。 请参阅[处理存储类驱动程序中的即插即用开始](handling-pnp-start-in-a-storage-class-driver.md)。

-   删除请求的响应中删除其设备 (IRP\_MJ\_IRP 与 PNP\_MN\_删除\_设备)。 请参阅[存储类驱动程序的 RemoveDevice 例程](storage-class-driver-s-removedevice-routine.md)。

-   如果其设备可以包含系统分页文件，维护的分页路径通知其设备扩展到寻呼通知请求的响应中的计数 (IRP\_MJ\_与 PNP [ **IRP\_MN\_设备\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)) 并将请求转发到下一步低驱动程序。

-   处理查询、 删除和查询停止请求，并且，如果设备包含系统页面文件或休眠文件，此类请求失败。 驱动程序可能还无法满足该查询删除请求如果其设备声明为故障转储，因为删除此类设备禁用故障转储。

存储类驱动程序将转发即插即用的查询、 cancel 和停止到下一步低驱动程序请求数 （除了失败的查询请求）。

 

 




