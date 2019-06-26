---
title: ACPI 设备的设备堆栈
description: ACPI 设备的设备堆栈
ms.assetid: f177d29f-eaf9-4126-8cb3-9355d977bfb0
keywords:
- ACPI 设备 WDK，设备堆栈
- 设备堆栈 WDK ACPI
- WDK ACPI 的功能的设备对象
- FDOs WDK ACPI
- 筛选 DOs WDK ACPI
- 根总线驱动程序 WDK ACPI
- 功能的驱动程序 WDK ACPI，设备堆栈
- WDM 函数驱动程序 WDK ACPI，设备堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a2befb4974b0ccee264317ea4189a3b7f4c4f47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355860"
---
# <a name="device-stacks-for-an-acpi-device"></a>ACPI 设备的设备堆栈





本部分介绍了包括一个可选功能的设备对象的设备堆栈 ACPI 设备 (*FDO*) 创建的供应商提供 WDM 功能驱动程序。

系统将创建一个系统的 ACPI 名称空间中的每个设备下图中所示的两个设备堆栈。

![两个关系图说明如何在左侧，筛选器执行操作，然后在右侧的 acpi 设备堆栈不包含筛选器的 acpi 设备堆栈执行操作](images/acpidev1.png)

如果 ACPI 设备集成到系统主板的硬件设备，系统会创建设备堆栈的总线筛选器设备对象 （筛选器执行操作）。 设备的物理设备对象 (*PDO*) 创建由系统提供根总线驱动程序和 ACPI 驱动程序创建总线筛选器执行操作。 筛选器执行操作的状态显示是透明的上面设备堆栈中的其他设备对象。

如果设备不是硬件设备集成到系统主板，ACPI 驱动程序枚举设备，并创建一个 PDO。 在任一情况下，供应商可以提供可选 FDO。

### <a name="system-supplied-root-bus-driver-and-acpi-driver"></a>系统提供根总线驱动程序和 ACPI 驱动程序

Microsoft 提供根总线驱动程序和[ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)。 在系统上具有 ACPI BIOS，HAL 会导致要在设备树中，它充当接口之间的操作系统和 BIOS 的系统启动期间加载的 ACPI 驱动程序。 ACPI 驱动程序是透明的其他驱动程序。

### <a name="vendor-supplied-function-driver"></a>驱动程序供应商提供的函数

供应商可以提供 ACPI 设备的可选 WDM 函数驱动程序。 功能驱动程序实现设备的操作区域和相关的特定于设备的操作。

 

 




