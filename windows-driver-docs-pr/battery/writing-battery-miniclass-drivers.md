---
title: 编写电池微型类驱动程序
description: 编写电池微型类驱动程序
keywords:
- 电池 miniclass 驱动程序 WDK
- 电池 miniclass 驱动程序 WDK，关于编写电池 miniclass 驱动程序
- 与设备无关的电池支持 WDK
- 设备特定电池支持 WDK
- 电池类驱动程序 WDK
- 电池类驱动程序 WDK，关于电池类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa8df2abd62d4b9ba6c9e4a297a7530b90e533c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784301"
---
# <a name="writing-battery-miniclass-drivers"></a>编写电池微型类驱动程序


## <span id="ddk_writing_battery_miniclass_drivers_dg"></span><span id="DDK_WRITING_BATTERY_MINICLASS_DRIVERS_DG"></span>


电池通常有一对驱动程序：Microsoft 提供的通用电池类驱动程序，以及专门为具体电池类型编写的小型驱动程序。

类驱动程序定义系统中电池的整体功能，并与电源管理器进行交互。

Miniclass 驱动程序处理特定于设备的功能，例如添加和取出电池，并跟踪其容量和电量。 Miniclass 驱动程序导出类驱动程序调用的例程，以获取有关它所控制设备的信息。

有关编写电池 miniclass 驱动程序的信息如下所示：

[系统电池管理概述](overview-of-system-battery-management.md)

[电池类和微型类驱动程序的交互](interaction-of-battery-class-and-miniclass-drivers.md)

[提供所需的电池微型类驱动程序功能](supplying-required-battery-miniclass-driver-functionality.md)

[电池微型类驱动程序的 DriverEntry 例程](driverentry-routine-of-a-battery-miniclass-driver.md)

[电池微型类驱动程序的 AddDevice 例程](adddevice-routine-of-a-battery-miniclass-driver.md)

[电池微型类驱动程序的 DispatchDeviceControl 例程](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[电池微型类驱动程序的 DispatchSystemControl 例程](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[响应电池类驱动程序查询](responding-to-battery-class-driver-queries.md)

[提供电池设备通知](supplying-battery-device-notification.md)

[电池微型类驱动程序的 Unload 例程](unload-routine-of-a-battery-miniclass-driver.md)

[安装电池驱动程序](installing-a-battery-driver.md)

 

 




