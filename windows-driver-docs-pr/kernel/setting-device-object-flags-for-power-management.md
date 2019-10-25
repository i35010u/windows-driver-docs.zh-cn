---
title: 为电源管理设置设备对象标志
description: 为电源管理设置设备对象标志
ms.assetid: 58d1a3a2-c8ea-446c-b1d6-ed00411d1d75
keywords:
- DO_POWER_PAGABLE
- DO_POWER_INRUSH
- 设备对象标志 WDK 电源管理
- 对象标志 WDK 电源管理
- 标志 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8424b17f14cb3cf878ebd47b958d9fa445f72c23
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836360"
---
# <a name="setting-device-object-flags-for-power-management"></a>为电源管理设置设备对象标志





在其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中，每个驱动程序都创建一个设备对象（筛选设备对象（DO）、功能设备对象（FDO）或物理设备对象（PDO）），并在设备对象中设置 DO\_*XXX*标志来描述设备属性和驱动程序配置。 以下设备对象标志与电源管理相关。

| 旗帜               | 描述                                                                                                                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \_电源\_浪涌  | 指示设备在首次打开时由设备电涌绘制的电流。 这一冲击或 "浪涌" 持续一小段时间，超过此时间后，设备的当前绘制时间将降到较低的操作级别。                                                                                   |
| \_POWER\_PAGABLE | 指示驱动程序可分页。 从 Windows 2000 开始，可以分页的驱动程序必须设置 DO\_POWER\_PAGABLE 标志。 电源管理器以 IRQL = 被动\_级别调用此类驱动程序。 有关可分页驱动程序的详细信息，请参阅[使驱动程序可分页](making-drivers-pageable.md)。 |

 

设备对象标志通常由总线驱动程序在创建设备的 PDO 时设置。 但是，某些函数驱动程序可能需要将这些标志的值作为其*AddDevice*例程的一部分进行更改。 从 Windows Vista 开始，操作系统不要求设备堆栈中的所有设备对象都具有相同的与电源相关的标志集。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，设备堆栈中的所有设备对象应具有相同的与电源相关的标志。

从 Windows 2000 开始，寻呼路径中的设备驱动程序不能设置 DO\_POWER\_PAGABLE 标志。 如果驱动程序参与了页面文件的 i/o 操作，则该驱动程序位于 "分页路径" 中。 未设置此标志的驱动程序必须可在 IRQL = 调度\_级别上调用。 有关详细信息，请参阅[调度例程的约束](https://docs.microsoft.com/windows-hardware/drivers/ifs/constraints-on-dispatch-routines)。

通常，驱动程序不应更改 DO\_POWER\_PAGABLE 标志的总线驱动程序的值，如果低级驱动程序清除了该标志，则驱动程序决不能设置此标志。 处理涉及[PnP 寻呼请求](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-pnp-paging-requests)的转换（通常是为了响应[**irp\_MJ\_PnP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp) with [**irp\_MN\_设备\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)请求），存储驱动程序必须仔细排序其设置并清除标志。

需要在启动时浪涌的设备的驱动程序必须先在设备对象中设置 DO\_POWER\_浪涌标志，然后才能清除 "执行\_设备\_初始化" 标志。 设备堆栈中仅有一个驱动程序通常是总线驱动程序（PDO），需要为设备设置 "DO\_POWER\_浪涌标志。 该标志通知电源管理器此类设备必须一次打开一次，并按与其他此类设备相同的顺序进行管理，以避免重载电源。 在任何给定时间，电源管理器都可确保系统中的任何位置都只有一个电源浪涌 IRP 处于活动状态。

从 Windows Vista 开始，驱动程序可以设置 DO\_POWER\_PAGABLE 标志和 DO\_POWER\_浪涌标志。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序不能同时设置 DO\_POWER\_PAGABLE 标志和 DO\_POWER\_浪涌标志。

 

 




