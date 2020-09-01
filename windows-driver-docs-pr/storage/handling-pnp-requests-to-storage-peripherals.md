---
title: 处理对存储外设的 PnP 请求
description: 处理对存储外设的 PnP 请求
ms.assetid: 9c7ea576-11e6-46d7-b04c-ce412a0fc569
keywords:
- 外围设备 WDK 存储、PnP 请求
- 存储外围设备 WDK、PnP 请求
- PnP WDK 存储
- 即插即用 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c834ce1fd344c31df4d443e585b693473b9ae03f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187541"
---
# <a name="handling-pnp-requests-to-storage-peripherals"></a>处理对存储外设的 PnP 请求


## <span id="ddk_handling_pnp_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_PNP_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


存储类驱动程序的 *DispatchPnP* 例程负责以下各项，以响应 PnP 请求：

-   启动其设备以响应启动请求 (IRP \_ MJ \_ PNP with irp \_ MN \_ start \_ device) 。 请参阅 [在存储类驱动程序中处理 PnP 启动](handling-pnp-start-in-a-storage-class-driver.md)。

-   删除其设备以响应删除请求 (IRP \_ MJ \_ PNP with irp \_ MN \_ remove \_ device) 。 请参阅 [存储类驱动程序的 RemoveDevice 例程](storage-class-driver-s-removedevice-routine.md)。

-   如果其设备可以包含系统分页文件，请在其设备扩展中维护寻呼路径通知，以响应寻呼通知请求 (IRP \_ MJ \_ PNP with [**irp \_ MN \_ 设备 \_ 使用 \_ 通知**](../kernel/irp-mn-device-usage-notification.md)) 并将请求转发到下一个较低的驱动程序。

-   处理查询-删除和查询停止请求，如果设备包含系统分页文件或休眠文件，则导致此类请求失败。 如果驱动程序的设备被声称崩溃转储，则驱动程序也可能会导致查询删除请求失败，因为删除此类设备会禁用故障转储。

存储类驱动程序将 "PnP 查询"、"取消" 和 "停止" 请求转发 (除了失败的查询请求) 到下一个较低的驱动程序。

 

