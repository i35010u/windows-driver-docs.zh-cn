---
title: ACPI 设备的设备堆栈
description: ACPI 设备的设备堆栈
ms.assetid: f177d29f-eaf9-4126-8cb3-9355d977bfb0
keywords:
- ACPI 设备 WDK，设备堆栈
- 设备堆栈 WDK ACPI
- 功能设备对象 WDK ACPI
- FDOs WDK ACPI
- 筛选 DOs WDK ACPI
- 根总线驱动程序 WDK ACPI
- 函数驱动程序 WDK ACPI，设备堆栈
- WDM 函数驱动程序 WDK ACPI，设备堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcf26d867a353a04a967e0e98da078d725849330
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184875"
---
# <a name="device-stacks-for-an-acpi-device"></a>ACPI 设备的设备堆栈





本部分介绍了 ACPI 设备的设备堆栈，其中包含由供应商提供的 WDM 函数驱动程序创建 (*FDO*) 的可选功能设备对象。

系统会为系统 ACPI 命名空间中的每个设备创建如下图所示的两个设备堆栈之一。

![下面两个关系图演示了一个具有筛选器的 acpi 设备堆栈，在右侧，没有筛选器的 acpi 设备堆栈执行](images/acpidev1.png)

如果 ACPI 设备是集成到系统板中的硬件设备，则系统会创建一个具有总线筛选器设备对象的设备堆栈 (筛选器执行) 。 设备的物理设备对象 (*PDO*) 由系统提供的根总线驱动程序创建，ACPI 驱动程序创建总线筛选器。 筛选器的存在对设备堆栈中的其他设备对象是透明的。

如果设备不是集成到系统板的硬件设备，则 ACPI 驱动程序会枚举设备并创建 PDO。 在任一情况下，供应商可以提供一个可选的 FDO。

### <a name="system-supplied-root-bus-driver-and-acpi-driver"></a>系统提供的根总线驱动程序和 ACPI 驱动程序

Microsoft 提供根总线驱动程序和 [ACPI 驱动程序](../kernel/acpi-driver.md)。 在具有 ACPI BIOS 的系统上，HAL 会使 ACPI 驱动程序在系统启动期间在设备树的基础上加载，在此过程中，它充当操作系统和 BIOS 之间的接口。 ACPI 驱动程序对其他驱动程序是透明的。

### <a name="vendor-supplied-function-driver"></a>供应商提供的函数驱动程序

供应商可以为 ACPI 设备提供可选的 WDM 函数驱动程序。 函数驱动程序实现设备的操作区域和相关的设备特定的操作。

 

