---
title: 电池微型类驱动程序的 AddDevice 例程
description: 电池微型类驱动程序的 AddDevice 例程
ms.assetid: 1b34e223-e238-4547-bd44-754be2e6749c
keywords:
- AddDevice 例程 WDK 电池
- 电池 miniclass 驱动程序 WDK，例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 047409777394f18b83f1484ddd107c53de627969
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335414"
---
# <a name="adddevice-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 AddDevice 例程


## <span id="ddk_adddevice_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_ADDDEVICE_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


每个电池 miniclass 驱动程序必须具有[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程，初始化特定于电池的状态。 PnP 管理器调用*AddDevice*例程的每个电池设备受此 miniclass 驱动程序。

除了所需的即插即用的任务*AddDevice*例程*AddDevice*例程电池 miniclass 驱动程序还必须执行以下操作：

1.  创建电池 FDO 并将 FDO 附加到的控制器设备堆栈。

2.  初始化[**电池\_微型端口\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff536287)结构和调用[ **BatteryClassInitializeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff536266)miniclass 驱动程序注册到电池类驱动程序。

3.  执行所需的设备的任何其他初始化。

 

 




