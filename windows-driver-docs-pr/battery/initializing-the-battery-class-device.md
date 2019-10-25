---
title: 初始化电池类设备
description: 初始化电池类设备
ms.assetid: d385533e-790a-47b3-a3d2-d620cbd40a4d
keywords:
- 电池类驱动程序 WDK，设备初始化
- 电池 miniclass 驱动程序 WDK，注册
- 注册电池设备
- 初始化电池设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f62d7119927220f90512f29a0bbefcb38d968f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832221"
---
# <a name="initializing-the-battery-class-device"></a>初始化电池类设备


## <span id="ddk_initializing_the_battery_class_device_dg"></span><span id="DDK_INITIALIZING_THE_BATTERY_CLASS_DEVICE_DG"></span>


[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程必须初始化电池类设备，并将 miniclass 驱动程序注册到类驱动程序。 为此，miniclass 驱动程序将调用[**BatteryClassInitializeDevice**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice)例程。 此调用向类驱动程序注册 miniclass 驱动程序，以便两个驱动程序可以使用彼此支持的例程。 此调用还会将电池设备注册到系统，以便复合电池和电源指示器可以观察到该设备。

**BatteryClassInitializeDevice**需要一个指向[**电池\_微型端口\_信息**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)结构的指针，其中包含以下信息：

-   在**MajorVersion**和**MinorVersion**中，此 miniclass 驱动程序支持的类驱动程序的主版本号和次版本号。

    版本号在 Batclass 中定义为 "电池\_类\_" 主要\_版本 "和" 电池\_类\_次要\_版本 "。

-   在**QueryTag**中，miniclass 驱动程序的[*BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)例程的入口点。

-   在**QueryInformation**中，miniclass 驱动程序的[*BatteryMiniQueryInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)例程的入口点。

-   在**SetInformation**中，miniclass 驱动程序的[*BatteryMiniSetInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_information_callback)例程的入口点。

-   在**SetStatusNotify**中，miniclass 驱动程序的[*BatteryMiniSetStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)例程的入口点。

-   在**DisableStatusNotify**中，miniclass 驱动程序的[*BatteryMiniDisableStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)例程的入口点。

-   在**上下文**中，是指向 miniclass 驱动程序的上下文信息的指针。

    上下文信息通常是一个指针，指向 FDO 设备扩展，每次类驱动程序调用[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)例程时，该扩展会传递回 miniclass 驱动程序。

-   在**pdo**中，指向设备的 Pdo 的指针。

-   在**DeviceName**中，为 NULL 参数;PnP 设备不应具有名称。

设置此结构后，miniclass 驱动程序会通过调用**BatteryClassInitializeDevice**将自身附加到电池类驱动程序，并将一个指针传递到电池\_微型端口\_信息结构。 在返回时，它会收到一个句柄，用于对电池类驱动程序支持例程的后续调用。 Miniclass 驱动程序应在非分页内存中存储返回的类句柄。

调用**BatteryClassInitializeDevice**后， [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程可能还需要初始化其他特定于设备的数据。

 

 




