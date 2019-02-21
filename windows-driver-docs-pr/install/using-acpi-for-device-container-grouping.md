---
title: ACPI 用于设备容器分组
description: ACPI 用于设备容器分组
ms.assetid: c49949cd-59e0-4ad2-a067-bc4e048f26c5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88106262ae3e4eaf9d2d280a3a6b70500a522c52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524248"
---
# <a name="using-acpi-for-device-container-grouping"></a>ACPI 用于设备容器分组


使用 ACPI 设置来指定设备容器分组被适用于使用由计算机原始设备制造商 (Oem)。 通过配置计算机 BIOS 中的 ACPI 对象，则可以指示计算机的精确的配置。 此功能不包括其他设备容器，用于分组在本文中介绍的机制。

ACPI 以指示该计算机的配置使用具有以下优点：

-   计算机 BIOS 中持久保存，在操作系统升级保留这些设置。

-   它的计算结果总线驱动程序提供可移动功能后，Windows 将计算 ACPI 设置。 因此，制造商可以使用 ACPI 设置以修复错误地报告为可移动设备和 Windows 可以分组到计算机的设备容器的功能。

-   使用 ACPI 设置是计算机 oem 以指示哪些 USB 端口都内置于计算机和哪些 USB 端口的用户是能够将附加外部设备特别有用。 有关详细信息，请参阅[到配置的计算机上的 USB 端口中使用 ACPI](using-acpi-to-configure-usb-ports-on-a-computer.md)。

    计算机 OEM 是计算机的强烈建议以配置要准确反映的 USB 端口拓扑的 ACPI BIOS 设置。 这可确保与以物理方式集成 USB 设备的计算机 （例如，内部的蓝牙无线或集成的网络摄像机） 分组到计算机的设备容器。 它还允许操作系统以更好地确定计算机和外部连接的设备之间的边界，因为设备连接到可连接/用户可见的端口被假定为外部设备。

有关如何使用 ACPI 对象设置的设备容器分组的详细信息，请参阅[在 Windows 7 中的容器分组](https://go.microsoft.com/fwlink/p/?linkid=158386)白皮书

 

 





