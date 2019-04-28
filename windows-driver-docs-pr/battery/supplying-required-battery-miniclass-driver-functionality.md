---
title: 提供所需的电池微型类驱动程序功能
description: 提供所需的电池微型类驱动程序功能
ms.assetid: d33d3c8c-f867-40dc-901c-6b0dd5d57dac
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- 例程 WDK 电池
- 电池 miniclass 驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b6e2464a483e233cc195e2c79887d1fbf5521b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335259"
---
# <a name="supplying-required-battery-miniclass-driver-functionality"></a>提供所需的电池微型类驱动程序功能


## <span id="ddk_supplying_required_battery_miniclass_driver_functionality_dg"></span><span id="DDK_SUPPLYING_REQUIRED_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


除了支持所需的例程[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)，电池 miniclass 驱动程序必须具有以下例程：

[DriverEntry](driverentry-routine-of-a-battery-miniclass-driver.md)

[AddDevice](adddevice-routine-of-a-battery-miniclass-driver.md)

[DispatchDeviceControl](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[DispatchSystemControl](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[*BatteryMiniQueryTag*](https://msdn.microsoft.com/library/windows/hardware/ff536275)

[*BatteryMiniQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff536274)

[*BatteryMiniQueryInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536273)

[*BatteryMiniSetInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536276)

[*BatteryMiniSetStatusNotify*](https://msdn.microsoft.com/library/windows/hardware/ff536277)

[*BatteryMiniDisableStatusNotify*](https://msdn.microsoft.com/library/windows/hardware/ff536272)

[卸载](unload-routine-of-a-battery-miniclass-driver.md)

[DriverEntry](driverentry-routine-of-a-battery-miniclass-driver.md)， [Unload](unload-routine-of-a-battery-miniclass-driver.md)， [DispatchDeviceControl](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)，并且[AddDevice](adddevice-routine-of-a-battery-miniclass-driver.md)是标准的驱动程序例程。 DriverEntry 的名称是必需的以便操作系统可以启动驱动程序时调用它。 可以选用其地址已经正确加载相应的数据结构中的其他驱动程序例程名称您自行决定。

[BatteryMini*Xxx* ](https://msdn.microsoft.com/library/windows/hardware/ff536286)例程都是由 miniclass 驱动程序提供，通过电池类驱动程序调用。 在编写 miniclass 驱动程序时，你可以选择不实现任何这些例程; 的功能但是，不过必须提供该例程的入口点，并且该例程必须返回状态\_不\_受支持。 这些例程的原型出现在 Batclass.h。

电池 miniclass 驱动程序必须包含以下标头文件：

-   Batclass.h

-   Ntddk.h 或 wdm.h 中

 

 




