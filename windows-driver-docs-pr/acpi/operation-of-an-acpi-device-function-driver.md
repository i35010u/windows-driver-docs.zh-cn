---
title: ACPI 设备函数驱动程序的操作
description: ACPI 设备函数驱动程序的操作
keywords:
- ACPI 设备 WDK，函数驱动程序操作
- 供应商提供的函数驱动程序 WDK ACPI
- 函数驱动程序 WDK ACPI，操作
- WDM 函数驱动程序 WDK ACPI，操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fe071b33f3d06828b824a6f29e4f554e72bcad3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789481"
---
# <a name="operation-of-an-acpi-device-function-driver"></a>ACPI 设备函数驱动程序的操作





本部分介绍了供应商为 ACPI 设备提供的函数驱动程序的一般操作。

ACPI 设备的函数驱动程序是执行以下操作的 WDM 驱动程序：

-   符合 WDM 函数驱动程序的最低要求，如 [Windows 驱动模型](../kernel/introduction-to-wdm.md)中所述。 这包括驱动程序入口点、调度例程、即插即用、电源管理和 Windows Management Instrumentation (WMI) 。 此基本功能提供 Windows 需要驱动程序的一般操作和用于实现 ACPI 设备特定操作的框架。

-   支持设备的操作区域，这是功能驱动程序和 ACPI BIOS 之间的通信接口。

    有关详细信息，请参阅[支持操作区域](supporting-an-operation-region.md)。

-   （可选）支持供应商定义的 *设备接口* ，并 *IOCTLs* 其他驱动程序或用户模式应用程序用于操作设备。

    有关详细信息，请参阅 [提供供应商定义的 ACPI 设备接口](providing-a-vendor-defined-acpi-device-interface.md)。

 

