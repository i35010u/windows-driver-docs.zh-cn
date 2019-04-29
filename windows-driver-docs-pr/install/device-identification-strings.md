---
title: 设备标识字符串
description: 插即用 (PnP) 管理器和其他设备安装组件使用设备标识字符串来标识计算机中安装的设备。
ms.assetid: dae23185-63d9-4a0f-9786-c7fa66368826
keywords:
- 兼容 Id WDK 设备安装
- 设备 Id WDK 设备安装
- 设备实例 Id WDK 设备安装
- 驱动程序节点 WDK 设备安装
- 硬件 Id WDK 设备安装
- 实例 Id WDK 设备安装
- 设备安装程序 WDK 设备安装，设备标识字符串
- 设备安装 WDK，设备标识字符串
- 安装设备 WDK，设备标识字符串
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8eb23f0e5429b26fff04f04c25d7e1135a7b4fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357811"
---
# <a name="device-identification-strings"></a>设备标识字符串

插即用 (PnP) 管理器和其他[设备安装组件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)使用设备标识字符串来识别计算机中安装的设备。

Windows 使用的以下设备标识字符串以查找最匹配的设备的信息 (INF) 文件。 由设备的枚举器，发现基于即插即用硬件标准的即插即用设备的系统组件，这些字符串进行报告。 这些任务都由即插即用总线驱动程序将在执行与 PnP 管理器的合作关系。 通常，设备会枚举由其父总线驱动程序，如 PCI 或 PCMCIA 总线驱动程序。 某些设备枚举由总线筛选器驱动程序，如 ACPI 驱动程序。

- [硬件 Id](hardware-ids.md)

- [兼容 Id](compatible-ids.md)

Windows 将尝试查找一个硬件 Id 或兼容 Id 的匹配项。 有关 Windows 如何使用这些 Id 来匹配设备 INF 文件，以及如何在 INF 文件中指定 Id 的详细信息，请参阅[Windows 中如何选择驱动程序](how-setup-selects-drivers.md)。

除了使用上述 Id 来标识设备，即插即用管理器使用以下 Id 来唯一标识每个设备的计算机中安装的实例：

- [实例 Id](instance-ids.md)

- [设备实例 Id](device-instance-ids.md)

从 Windows 7 开始，即插即用管理器使用[容器 ID](container-ids.md)设备标识字符串进行分组的一个或多个设备 (devnodes) 的节点已枚举从计算机中安装的物理设备的每个实例。

每个枚举器自定义其设备 Id、 硬件 Id 和兼容 Id 来唯一标识它枚举设备。 此外，每个枚举器具有其自己的策略，以确定硬件 Id 和兼容 Id。 有关硬件 ID 和兼容 ID 格式的大部分系统总线的详细信息，请参阅[设备标识符格式](device-identifier-formats.md)。
