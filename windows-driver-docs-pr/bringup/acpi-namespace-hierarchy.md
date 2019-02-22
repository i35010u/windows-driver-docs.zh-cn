---
title: ACPI 命名空间层次结构
description: ACPI 命名空间层次结构必须准确地建模平台的硬件拓扑，从处理器的系统总线 (\ 0034;\\_SB \ 0034;)。
ms.assetid: 14B5F787-65B1-4BC3-90CD-D4AD1C8044D1
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: ef292aa814845a758fd29ead682b525250e1a4a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534586"
---
# <a name="acpi-namespace-hierarchy"></a>ACPI 命名空间层次结构


ACPI 命名空间层次结构必须准确地建模平台的硬件拓扑，从处理器的系统总线 ("\\\_SB")。 一般情况下，连接到总线或控制器的设备显示为该总线或控制器设备命名空间中的子项。

以下规则适用于 SoC 基于平台：

-   内存映射功能块 （包括处理器） 显示正下方\\ \_SB 节点。
-   连接到的简单外围总线 （存储） 控制器和/或 GPIO 控制器某些组合的外围设备描述连接资源为其连接到这些域控制器。 有关详细信息，请参阅[常规用途 I/O (GPIO)](general-purpose-i-o--gpio-.md)并[简单外围总线 （存储）](simple-peripheral-bus--spb-.md)。

    在这种方式中的连接的外围设备直接下面可能会出现\\ \_SB 节点，或在父存储或 GPIO 控制器。 后者是首选方法，如果可能，因为它指示直接在该命名空间本身，而不是请求的资源，以发现的关系解码中的设备关系。

-   任何功能块或通过支持硬件枚举 （例如，SDIO 和 USB） 的标准总线连接的外围设备不需要完全显示命名空间中。

    但是，您必须在某些情况下命名空间中包含其父控制器下的此类设备。 例如，这是必要的 embedded USB HSIC 或 SDIO 设备，在使用特定于平台的 （非标准） 控件 （例如，电源开关、 GPIO 或存储连接时，等），作为系统设计的一部分是与设备相关联。 在这种情况下，标准父总线驱动程序枚举设备，但[Windows ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)，作为要调用的非标准控件代表总线驱动程序的控制方法的设备堆栈中的筛选器加载 Acpi.sys，根据需要。

-   任何"private"的总线或专用于一个功能驱动程序 （例如，音频驱动程序） 使用的设备 (例如，I2S) 不需要完全显示命名空间中。 但是，在这种情况下，设备使用的任何系统资源必须出现在命名空间中的函数设备的资源列表。 有关详细信息，请参阅**设备配置对象**主题中[设备管理命名空间对象](device-management-namespace-objects.md)主题。

ACPI 定义了许多标准命名空间对象和方法，但在需要实施者可以定义新的。 ACPI 定义的对象和方法用于常见操作系统函数，如下所示：

*平台说明*例如，包括设备标识和系统资源分配。

*通用设备控制*例如配置资源和控制 power 资源。

*特定于类功能控制*变暗显示或报告的电池状态等。


