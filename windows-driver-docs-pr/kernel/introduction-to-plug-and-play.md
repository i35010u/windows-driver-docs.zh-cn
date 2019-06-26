---
title: 即插即用简介
description: 即插即用简介
ms.assetid: 2ad9663b-ea47-4f7a-a382-53de3719214b
keywords:
- 有关即插即插即用 WDK 内核
- 有关即插即插 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50b7c9ebc4370f3c2f207443451e15cff88abe01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369917"
---
# <a name="introduction-to-plug-and-play"></a>即插即用简介





插即用 (PnP) 是可让计算机系统识别并调整用户很少或没有干预的硬件配置更改的硬件和软件支持的组合。 用户可以添加到设备和计算机系统中删除设备，而不必执行令人费解和令人困惑的手动配置，而无需复杂的计算机硬件知识。 例如，用户可以停靠便携式计算机和使用扩展坞键盘、 鼠标和监视器无需进行手动配置更改。

即插即用需要支持的设备硬件、 系统软件和驱动程序。 计划硬件行业中的定义的外接程序主板和基本系统组件上的方便识别 （例如即插即用 ISA 定义和标准 PC 卡） 标准。 文档集中说明了系统软件对此 Windows Driver Kit (WDK) PnP 和 PnP 驱动程序使用该功能的支持来实现的方式。

系统软件支持的 PnP，与即插即用驱动程序一起提供了以下：

-   自动和动态识别的已安装硬件

    系统软件在初始系统安装过程可识别硬件，可以识别之间系统启动时，发生并对运行时硬件事件，例如停靠或移除和设备插入或删除作出响应的即插即用硬件更改。

-   硬件资源分配 （和重新分配）

    PnP 管理器确定请求的每个设备的硬件资源 (例如，输入/输出端口\[I/O\]，中断请求\[Irq\]，直接内存访问\[DMA\]通道和内存位置)，并将相应地分配硬件资源。 PnP 管理器重新配置资源分配，如有必要，例如当新设备添加到系统，需要已在使用的资源。

    即插即用设备的驱动程序不分配资源;相反，当枚举设备时标识设备的请求的资源。 PnP 管理器在资源分配期间检索每个设备的要求。 资源不可以为旧设备、 动态配置，因此 PnP 管理器中向资源首先分配到原有的设备。

-   正在加载的合适的驱动程序

    PnP 管理器确定支持的每个设备所需的驱动程序，并加载这些驱动程序。

-   与即插即用系统进行交互的驱动程序适用的编程接口

    该接口包含[I/O 管理器例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551797(v=vs.85))，[即插即用次要 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)、 所需[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)，并在注册表中的信息。

-   机制来驱动程序和应用程序以了解硬件环境中的更改并采取相应的措施

    即插即用可使驱动程序和用户模式代码进行注册，并收到的某些硬件事件通知。

即插即用驱动程序是即插即用支持的一个重要部分。 对于像 PnP 它使符合标准的驱动程序必须提供所需的即插即用入口点、 处理所需的 PnP Irp，然后按照即插即用指导。

本部分包含以下其他主题：

[即插即用组件](pnp-components.md)

[PnP 的支持级别](levels-of-support-for-pnp.md)

[即插即用驱动程序设计指南](pnp-driver-design-guidelines.md)

[设备树](device-tree.md)

[硬件资源](hardware-resources.md)

[即插即用设备的状态转换](state-transitions-for-pnp-devices.md)

 

 




