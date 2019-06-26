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
ms.openlocfilehash: 2e8d67ffe55c3e00b9220ab3e9c60e6a67f2d989
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385244"
---
# <a name="setting-device-object-flags-for-power-management"></a>为电源管理设置设备对象标志





在其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程，每个驱动程序创建一个设备对象 （筛选设备对象 （执行）、 功能的设备对象 (FDO) 或物理设备对象 (PDO)） 并设置执行\_*XXX*设备对象来描述的设备属性和驱动程序配置中的标志。 以下设备对象标志与电源管理有关。

| Flag               | 描述                                                                                                                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 不要\_电源\_浪涌  | 指示第一个设备时，由设备激增绘制当前打开。 此激增或"浪涌"持续在短时间内，在其后绘制的设备当前降到较低的运行级别。                                                                                   |
| 不要\_电源\_PAGABLE | 指示该驱动程序可分页。 从 Windows 2000 开始，可以分页的驱动程序必须设置 DO\_电源\_PAGABLE 标志。 电源管理器调用此类驱动程序在 IRQL = 被动\_级别。 有关可分页的驱动程序的详细信息，请参阅[使驱动程序可分页](making-drivers-pageable.md)。 |

 

创建的是 PDO 设备时，总线驱动程序通常会设置设备对象标志。 但是，某些功能的驱动程序可能需要更改这些标志的值作为的一部分他们*AddDevice*例程。 从 Windows Vista 开始，操作系统不需要设备堆栈中的所有设备对象都具有相同的与电源相关标志设置。 但是，在 Windows Server 2003、 Windows XP 和 Windows 2000，设备堆栈中的所有设备对象应都具有设置的相同电源相关标志。

从 Windows 2000 开始，都分页路径中的设备的驱动程序必须未设置 DO\_电源\_PAGABLE 标志。 驱动程序是"分页路径"中，如果它参与了分页文件上的 I/O 操作。 未设置此标志的驱动程序必须是可调用在 IRQL = 调度\_级别。 有关详细信息，请参阅[调度例程的约束](https://docs.microsoft.com/windows-hardware/drivers/ifs/constraints-on-dispatch-routines)。

一般情况下，驱动程序不应改变总线驱动程序的值对于，请执行\_电源\_PAGABLE 标志和一个驱动程序必须永远不会设置此标志如果较低级驱动程序已清除。 当处理工作交接涉及[PnP 分页请求](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-pnp-paging-requests)(通常以响应[ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)与[**IRP\_MN\_设备\_用法\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)请求)，存储驱动程序必须仔细序列它自身的设置和清除的标志。

需要在启动时 power 浪涌的设备的驱动程序必须设置 DO\_电源\_之前清除执行操作的设备对象中的浪涌标志\_设备\_正在初始化标志。 设备堆栈，通常的总线驱动程序 (PDO) 中只有一个驱动程序所需设置了\_电源\_浪涌标志的设备。 该标志通知此类设备必须注册一次一个地支持与其他此类设备，以避免重载电源供应的序列中的电源管理器。 电源管理器可确保在任何给定时间，只有一个电源浪涌 IRP 是系统中的任意位置激活。

从 Windows Vista 开始，驱动程序可以设置这两个执行操作\_电源\_PAGABLE 标志并执行\_POWER\_浪涌标志。 在 Windows Server 2003、 Windows XP 和 Windows 2000，驱动程序不能设置这两个执行操作\_电源\_PAGABLE 标志并执行\_POWER\_浪涌标志。

 

 




