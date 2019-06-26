---
title: 支持 ACPI 设备
description: 支持 ACPI 设备
ms.assetid: ebaf2e66-4f56-48ca-93ca-f34e694c0d73
keywords:
- 高级的配置和电源接口规范 WDK
- ACPI 设备 WDK
- ACPI 设备 WDK，关于 ACPI 设备
- 定义将阻止 WDK ACPI
- 操作区域 WDK ACPI
- 所需的操作区域处理 WDK ACPI
- 功能的驱动程序 WDK ACPI
- WDM 函数驱动程序 WDK ACPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e12356fa23256abf0a4e9692876f24a56afa56a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355806"
---
# <a name="supporting-acpi-devices"></a>支持 ACPI 设备


本部分介绍如何供应商可以使用 WDM 功能驱动程序在 Windows 中功能增强的功能的高级配置和电源接口 (ACPI) 设备。

ACPI 设备包括低级别系统设备，如电池、 热量区域和其他系统的 ACPI 名称空间中定义的设备。 ACPI 名称空间是 ACPI BIOS 用于引用对象的分层命名空间。

系统提供的组合的操作[ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)和 ACPI BIOS 支持 ACPI 设备的基本功能并对操作系统的其余部分是透明的。 ACPI 设备指定由 ACPI 系统描述表中的定义块。 此外，设备的定义块指定的操作区域，指定用来访问设备数据的设备内存的连续块。

若要增强的 ACPI 设备功能，供应商可以提供与通过提供由驱动程序的操作区域 ACPI BIOS 通信 WDM 功能驱动程序。 ACPI 驱动程序通过调用提供的功能驱动程序的操作区域处理程序来访问运营区域。

通过通信通过 ACPI 操作区域，功能驱动程序可以间接访问设备通常仅由 BIOS、 控制和 BIOS 可调用依赖于驱动程序和主机系统的配置的特定于设备的操作。 基本的运行机制是按如下所示：

1.  ACPI BIOS 读取或写入设备的操作区域中的数据。

2.  若要访问的操作区域，ACPI 驱动程序调用功能驱动程序的操作区域处理程序。

3.  操作区域处理程序执行任何操作进行编程访问，并返回具有访问权限相关联的信息。

以下两个示例演示一个供应商如何使用功能驱动程序来增强 ACPI 设备的功能：

1.  ACPI 设备可以访问会导致驱动程序以启用在供应商的预安装软件的声卡音量控件的功能驱动程序的操作区域中的索引。

2.  该驱动程序监视的电池、 热量区域的温度和通常是其他操作的剩余容量只有 BIOS 的访问。

以下主题介绍如何提供 ACPI 设备功能驱动程序：

[ACPI 设备的设备堆栈](device-stacks-for-an-acpi-device.md)

[ACPI 设备功能驱动程序的操作](operation-of-an-acpi-device-function-driver.md)

有关系统提供支持例程，支持 ACPI 设备功能的驱动程序，请参阅[ACPI 操作区域处理程序引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_acpi/index)。

有关 ACPI 设备和命名空间的详细信息，请参阅[高级配置和电源接口 (ACPI) 规范](https://go.microsoft.com/fwlink/p/?linkid=866846)。
