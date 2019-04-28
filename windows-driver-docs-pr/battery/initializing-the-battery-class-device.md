---
title: 初始化电池类设备
description: 初始化电池类设备
ms.assetid: d385533e-790a-47b3-a3d2-d620cbd40a4d
keywords:
- 电池类驱动程序 WDK，设备的初始化
- 电池 miniclass 驱动程序 WDK，注册
- 电池设备注册
- 初始化电池设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8de76e984768e09fef10b3ac892a6ac52cc1c3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335338"
---
# <a name="initializing-the-battery-class-device"></a>初始化电池类设备


## <span id="ddk_initializing_the_battery_class_device_dg"></span><span id="DDK_INITIALIZING_THE_BATTERY_CLASS_DEVICE_DG"></span>


[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程必须初始化电池类设备，并通过类驱动程序注册 miniclass 驱动程序。 若要执行此操作，miniclass 驱动程序调用[ **BatteryClassInitializeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff536266)例程。 此调用注册 miniclass 驱动程序类驱动程序，以便两个驱动程序可以使用其他的支持例程。 此调用还向系统注册电池设备，以便通过复合电池和电源表，可以查看它。

**BatteryClassInitializeDevice**需要指向的指针[**电池\_微型端口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536287)结构，其中包含以下信息：

-   在中**MajorVersion**并**MinorVersion**，此 miniclass 驱动程序支持的类驱动程序的主版本号和次版本号。

    在电池作为 Batclass.h 中定义的版本号\_类\_主要\_版本和电池\_类\_次要\_版本，分别。

-   在中**QueryTag**，miniclass 驱动程序的入口点[ *BatteryMiniQueryTag* ](https://msdn.microsoft.com/library/windows/hardware/ff536275)例程。

-   在中**QueryInformation**，miniclass 驱动程序的入口点[ *BatteryMiniQueryInformation* ](https://msdn.microsoft.com/library/windows/hardware/ff536273)例程。

-   在中**SetInformation**，miniclass 驱动程序的入口点[ *BatteryMiniSetInformation* ](https://msdn.microsoft.com/library/windows/hardware/ff536276)例程。

-   在中**SetStatusNotify**，miniclass 驱动程序的入口点[ *BatteryMiniSetStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536277)例程。

-   在中**DisableStatusNotify**，miniclass 驱动程序的入口点[ *BatteryMiniDisableStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536272)例程。

-   在中**上下文**，指向 miniclass 驱动程序的上下文信息的指针。

    上下文信息通常是指向每次调用的类驱动程序传递回 miniclass 驱动程序的 FDO 设备扩展[BatteryMini*Xxx* ](https://msdn.microsoft.com/library/windows/hardware/ff536286)例程。

-   在中**Pdo**，指向设备 PDO 的指针。

-   在中**DeviceName**，NULL 参数;即插即用设备不应具有名称。

设置此结构之后, miniclass 驱动程序将其自身附加到电池类驱动程序通过调用**BatteryClassInitializeDevice**，并将指针传递到电池\_微型端口\_信息结构。 反过来，它接收到电池类驱动程序支持例程的后续调用中使用的句柄。 Miniclass 驱动程序应在非分页内存中存储返回的类句柄。

在调用**BatteryClassInitializeDevice**，则[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程可能还需要初始化其他特定于设备的数据。

 

 




