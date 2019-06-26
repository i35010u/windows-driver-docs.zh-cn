---
title: ACPI 设备函数驱动程序的操作
description: ACPI 设备函数驱动程序的操作
ms.assetid: 56c63373-5094-4ae5-a7b0-56d61e3fa9b1
keywords:
- ACPI 设备 WDK，函数驱动程序操作
- 供应商提供的函数的 WDK ACPI 驱动程序
- 功能的驱动程序 WDK ACPI，操作
- WDM 函数驱动程序 WDK ACPI，操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f837b1126b5cf520b8c38d3df88a6a0feaa581ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355834"
---
# <a name="operation-of-an-acpi-device-function-driver"></a>ACPI 设备函数驱动程序的操作





本部分介绍的 ACPI 设备供应商提供的函数驱动程序的一般操作。

ACPI 设备功能驱动程序是 WDM 驱动程序，执行以下任务：

-   符合 WDM 功能驱动程序的最低要求，如中所述[Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)。 这包括驱动程序入口点、 调度例程、 插、 电源管理和 Windows Management Instrumentation (WMI)。 此基本功能可提供泛型操作该 Windows 需要的驱动程序和框架中实现 ACPI 特定于设备的操作。

-   支持设备的操作区域，这是功能驱动程序和 ACPI BIOS 之间的通信接口。

    有关详细信息，请参阅[支持运营区域](supporting-an-operation-region.md)。

-   （可选） 支持供应商定义*设备接口*并*Ioctl* ，其他驱动程序或用户模式应用程序使用来操作设备。

    有关详细信息，请参阅[提供 Vendor-Defined ACPI 设备接口](providing-a-vendor-defined-acpi-device-interface.md)。

 

 




