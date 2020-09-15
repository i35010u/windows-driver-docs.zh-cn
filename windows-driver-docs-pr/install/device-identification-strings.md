---
title: 设备标识字符串
description: 即插即用 (PnP) 管理器和其他设备安装组件使用设备标识字符串来识别安装在计算机上的设备。
ms.assetid: dae23185-63d9-4a0f-9786-c7fa66368826
keywords:
- 兼容 Id WDK 设备安装
- 设备 Id WDK 设备安装
- 设备实例 Id WDK 设备安装
- 驱动程序节点 WDK 设备安装
- 硬件 Id WDK 设备安装
- 实例 Id WDK 设备安装
- 设备设置 WDK 设备安装，设备标识字符串
- 设备安装 WDK，设备标识字符串
- 安装设备 WDK，设备标识字符串
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d1159c2436e7a518819287869cd595dd92968d7
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101460"
---
# <a name="device-identification-strings"></a>设备标识字符串

即插即用 (PnP) 管理器和其他 [设备安装组件](./overview-of-device-and-driver-installation.md) 使用设备标识字符串来识别安装在计算机上的设备。

Windows 使用以下设备标识字符串来查找与设备最匹配 (INF) 文件的信息。 这些字符串由设备的枚举器报告，系统组件基于 PnP 硬件标准发现 PnP 设备。 这些任务由与 PnP 管理器合作的 PnP 总线驱动程序执行。 设备通常由其父总线驱动程序（如 PCI 或 PCMCIA 总线驱动程序）枚举。 某些设备由总线筛选器驱动程序（如 ACPI 驱动程序）枚举。

- [硬件 Id](hardware-ids.md)

- [兼容 Id](compatible-ids.md)

Windows 尝试查找其中一个硬件 Id 或兼容 Id 的匹配项。 有关 Windows 如何使用这些 Id 将设备与 INF 文件相匹配的详细信息，以及如何在 INF 文件中指定 Id 的详细信息，请参阅 [Windows 如何选择驱动程序](./how-windows-selects-a-driver-for-a-device.md)。

除了使用前面的 Id 来标识设备之外，PnP 管理器还使用以下 Id 来唯一标识计算机上安装的每个设备的实例：

- [实例 Id](instance-ids.md)

- [设备实例 Id](device-instance-ids.md)

从 Windows 7 开始，PnP 管理器使用 [容器 ID](container-ids.md) 设备标识字符串对一个或多个设备节点进行分组， (devnodes) 从计算机上安装的每个物理设备实例枚举。

每个枚举器自定义其设备 Id、硬件 Id 和兼容 Id 以唯一标识它所枚举的设备。 此外，每个枚举器都有自己的策略来识别硬件 Id 和兼容 Id。 有关大多数系统总线的硬件 ID 和兼容 ID 格式的详细信息，请参阅 [设备标识符格式](./generic-identifiers.md)。

> [!NOTE]
> 不应分析设备标识字符串。 它们仅适用于字符串比较，应视为不透明字符串。