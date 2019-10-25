---
title: 支持 ACPI 设备
description: 支持 ACPI 设备
ms.assetid: ebaf2e66-4f56-48ca-93ca-f34e694c0d73
keywords:
- 高级配置和电源接口规范 WDK
- ACPI 设备 WDK
- ACPI 设备 WDK，关于 ACPI 设备
- 定义块 WDK ACPI
- 操作区域 WDK ACPI
- 操作区域处理程序 WDK ACPI
- 函数驱动程序 WDK ACPI
- WDM 函数驱动程序 WDK ACPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6f7281617d6143c544f67b797f4bfd02b6d567e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831444"
---
# <a name="supporting-acpi-devices"></a>支持 ACPI 设备


本部分介绍如何在 Windows 中使用 WDM 函数驱动程序来增强高级配置和电源接口（ACPI）设备的功能。

ACPI 设备包括低级别系统设备，如电池、热区和系统 ACPI 命名空间中定义的其他设备。 ACPI 命名空间是 ACPI BIOS 用来引用对象的分层命名空间。

系统提供的[acpi 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)和 acpi BIOS 的组合操作支持 acpi 设备的基本功能，并且对于操作系统的其余部分是透明的。 ACPI 设备由 ACPI 系统说明表中的定义块指定。 设备的定义块指定了一个操作区域，其中指定了用于访问设备数据的连续设备内存块。

若要增强 ACPI 设备的功能，供应商可以提供 WDM 函数驱动程序，该驱动程序通过驱动程序提供的操作区域与 ACPI BIOS 通信。 ACPI 驱动程序通过调用由函数驱动程序提供的操作区域处理程序来访问操作区域。

通过 ACPI 操作区域通信，函数驱动程序可以间接访问通常仅由 BIOS 控制的设备，并且 BIOS 可以调用特定于设备的操作，这些操作依赖于驱动程序和主机系统的配置。 基本操作机制如下：

1.  ACPI BIOS 在设备的操作区域中读取或写入数据。

2.  为了访问操作区域，ACPI 驱动程序调用函数驱动程序的操作区域处理程序。

3.  操作区域处理程序执行为访问编程的任何操作，并返回与访问关联的信息。

以下两个示例演示了供应商如何使用函数驱动程序增强 ACPI 设备的功能：

1.  ACPI 设备可以访问功能驱动程序的操作区域中的索引，该索引会导致驱动程序启用供应商预安装软件的声卡音量控制。

2.  驱动程序监视电池的剩余容量、热区的温度，以及通常仅由 BIOS 访问的其他东西。

以下主题介绍如何为 ACPI 设备提供函数驱动程序：

[ACPI 设备的设备堆栈](device-stacks-for-an-acpi-device.md)

[ACPI 设备函数驱动程序的操作](operation-of-an-acpi-device-function-driver.md)

有关系统提供的支持 ACPI 设备功能驱动程序的支持例程的信息，请参阅[ACPI 操作区域处理程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_acpi/index)。

有关 ACPI 设备和命名空间的详细信息，请参阅[高级配置和电源接口（ACPI）规范](https://go.microsoft.com/fwlink/p/?linkid=866846)。
