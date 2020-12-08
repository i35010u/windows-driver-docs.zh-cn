---
title: 为电源管理设置设备对象标志
description: 为电源管理设置设备对象标志
keywords:
- DO_POWER_PAGABLE
- DO_POWER_INRUSH
- 设备对象标志 WDK 电源管理
- 对象标志 WDK 电源管理
- 标志 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0131077342563cf6f3f346ad7a3ada27498defb1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822257"
---
# <a name="setting-device-object-flags-for-power-management"></a>为电源管理设置设备对象标志





在 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中，每个驱动程序都 (筛选器设备对象创建一个设备对象 (执行) 、功能设备对象 (FDO) 或物理设备对象 (PDO) # A7，并在 \_ 设备对象中设置 DO *XXX* 标记，以描述设备属性和驱动程序配置。 以下设备对象标志与电源管理相关。

| 标志               | 描述                                                                                                                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 执行 \_ 电源 \_ 浪涌  | 指示设备在首次打开时由设备电涌绘制的电流。 这一冲击或 "浪涌" 持续一小段时间，超过此时间后，设备的当前绘制时间将降到较低的操作级别。                                                                                   |
| 执行 \_ POWER \_ PAGABLE | 指示驱动程序可分页。 从 Windows 2000 开始，可以分页的驱动程序必须设置 DO \_ POWER \_ PAGABLE 标志。 电源管理器以 IRQL = 被动级别调用此类驱动程序 \_ 。 有关可分页驱动程序的详细信息，请参阅 [使驱动程序可分页](making-drivers-pageable.md)。 |

 

设备对象标志通常由总线驱动程序在创建设备的 PDO 时设置。 但是，某些函数驱动程序可能需要将这些标志的值作为其 *AddDevice* 例程的一部分进行更改。 从 Windows Vista 开始，操作系统不要求设备堆栈中的所有设备对象都具有相同的与电源相关的标志集。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，设备堆栈中的所有设备对象应具有相同的与电源相关的标志。

从 Windows 2000 开始，寻呼路径中的设备驱动程序不能设置 DO \_ POWER \_ PAGABLE 标志。 如果驱动程序参与了页面文件的 i/o 操作，则该驱动程序位于 "分页路径" 中。 未设置此标志的驱动程序必须可在 IRQL = 调度 \_ 级别调用。 有关详细信息，请参阅 [调度例程的约束](../ifs/constraints-on-dispatch-routines.md)。

通常情况下，驱动程序不应更改 DO POWER PAGABLE 标志的总线驱动程序的值 \_ \_ ，并且如果较低级别的驱动程序清除了此标志，则驱动程序决不能设置此标志。 处理涉及 [PnP 寻呼请求](../storage/handling-pnp-paging-requests.md) 的转换时 (通常是为了响应 [**irp \_ MJ \_ PnP**](./irp-mj-pnp.md) ，并使用 [**irp \_ MN \_ 设备 \_ 使用 \_ 通知**](./irp-mn-device-usage-notification.md) 请求) ，存储驱动程序必须仔细地对其设置进行排序并清除标志。

需要在启动时浪涌的设备的驱动程序必须在 \_ 设备对象中设置 "do power \_ 浪涌" 标志，然后清除 "执行 \_ 设备初始化" \_ 标志。 设备堆栈中仅有一个驱动程序，通常 (PDO) 的总线驱动程序需要设置设备的 "执行 \_ 电源 \_ 浪涌" 标志。 该标志通知电源管理器此类设备必须一次打开一次，并按与其他此类设备相同的顺序进行管理，以避免重载电源。 在任何给定时间，电源管理器都可确保系统中的任何位置都只有一个电源浪涌 IRP 处于活动状态。

从 Windows Vista 开始，驱动程序可以设置 DO \_ power \_ PAGABLE 标志和 do \_ power \_ 浪涌标志。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序不能同时设置 DO \_ power \_ PAGABLE 标志和 do \_ power \_ 浪涌标志。

 

