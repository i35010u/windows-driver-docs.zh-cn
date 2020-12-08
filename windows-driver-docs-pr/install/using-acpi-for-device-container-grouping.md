---
title: 将 ACPI 用于设备容器分组
description: 将 ACPI 用于设备容器分组
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 380e44b26ade57048182babd054d00d624442082
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805453"
---
# <a name="using-acpi-for-device-container-grouping"></a>将 ACPI 用于设备容器分组


使用 ACPI 设置指定设备容器分组旨在供计算机原始设备制造商 (Oem) 使用。 通过在计算机 BIOS 中配置 ACPI 对象，可以指示计算机的精确配置。 除了本文中所述的其他设备容器分组机制外，此功能也是如此。

使用 ACPI 指示计算机配置有以下优点：

-   这些设置在计算机 BIOS 中保持不变，并在操作系统升级时保留。

-   Windows 在评估了由总线驱动程序提供的可移动功能后评估 ACPI 设置。 因此，制造商可以使用 ACPI 设置来修复错误报告为可移动的设备，Windows 可以将功能分组到计算机的设备容器中。

-   使用 ACPI 设置对于计算机 Oem 来说特别有用，用来指示计算机内部的 USB 端口以及用户能够连接到外部设备的 USB 端口。 有关详细信息，请参阅 [使用 ACPI 配置计算机上的 USB 端口](using-acpi-to-configure-usb-ports-on-a-computer.md)。

    强烈建议计算机 OEM 配置 ACPI BIOS 设置，以准确反映计算机的 USB 端口拓扑。 这可确保将 USB 设备与计算机物理集成 (例如，将内部蓝牙无线电或集成的网络摄像机) 组合到计算机的设备容器中。 它还允许操作系统更好地确定计算机和外部连接的设备之间的边界，因为连接到可连接/用户可见端口的设备被假定为外部设备。

有关如何使用 ACPI 对象设置进行设备容器分组的详细信息，请参阅[Windows 7 白皮书中的容器分组](https://go.microsoft.com/fwlink/p/?linkid=158386)

 

 





