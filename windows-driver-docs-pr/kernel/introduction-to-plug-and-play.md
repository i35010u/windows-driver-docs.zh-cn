---
title: 即插即用简介
description: 即插即用简介
ms.assetid: 2ad9663b-ea47-4f7a-a382-53de3719214b
keywords:
- PnP WDK 内核，关于即插即用
- 即插即用 WDK 内核，关于即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 438037e237ec276ac999c1512b32b1082746e549
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192683"
---
# <a name="introduction-to-plug-and-play"></a>即插即用简介





即插即用 (PnP) 是硬件和软件支持的组合，这使计算机系统能够识别并适应用户对硬件配置所做的更改。 用户可以在计算机系统中添加设备并从中删除设备，而无需执行复杂且难以理解的手动配置，并且无需了解复杂的计算机硬件。 例如，用户可以在不进行手动配置更改的情况下，插接便携式计算机并使用插接站键盘、鼠标和监视器。

PnP 需要设备硬件、系统软件和驱动程序的支持。 硬件行业中的方案定义了标准 (例如 PnP ISA 定义和 PC 卡标准) ，以便轻松识别外接板和基本系统组件。 此 Windows 驱动程序工具包 (WDK) 文档重点介绍适用于 PnP 的系统软件支持以及驱动程序如何使用该支持来实现 PnP。

PnP 的系统软件支持与 PnP 驱动程序一起提供以下内容：

-   自动和动态识别已安装的硬件

    系统软件在初始系统安装期间识别硬件，识别在系统启动之间发生的 PnP 硬件更改，并响应运行时硬件事件，例如插接或移除以及设备插入或删除。

-   硬件资源分配 (和重新分配) 

    PnP 管理器会确定每个设备请求的硬件资源 (例如，输入/输出端口 \[ i/o \] 、中断请求 \[ irq \] 、直接内存访问 \[ DMA \] 通道和内存位置) 并适当地分配硬件资源。 必要时，PnP 管理器会重新配置资源分配，如将新设备添加到需要已使用资源的系统时。

    PnP 设备的驱动程序不分配资源;而是在枚举设备时标识设备的请求资源。 PnP 管理器检索资源分配过程中每个设备的要求。 对于旧设备，无法动态配置资源，因此 PnP 管理器首先将资源分配给旧设备。

-   加载相应的驱动程序

    PnP 管理器确定支持每个设备并加载这些驱动程序所需的驱动程序。

-   用于与 PnP 系统交互的驱动程序的编程接口

    该接口包含 [i/o 管理器例程](/previous-versions/windows/hardware/drivers/ff551797(v=vs.85))， [即插即用次 irp](./plug-and-play-minor-irps.md)，必需的 [标准驱动程序例程](./introduction-to-standard-driver-routines.md)，以及注册表中的信息。

-   驱动程序和应用程序用于了解硬件环境中的变化并采取适当措施的机制

    PnP 允许驱动程序和用户模式代码注册特定硬件事件并向其发送通知。

PnP 驱动程序是 PnP 支持的重要组成部分。 要使驱动程序符合 PnP 要求，必须提供所需的 PnP 入口点，处理所需的 PnP Irp，并遵循 PnP 指导原则。

本部分包含以下其他主题：

[PnP 组件](pnp-components.md)

[PnP 的支持级别](levels-of-support-for-pnp.md)

[PnP 驱动程序设计指导原则](pnp-driver-design-guidelines.md)

[设备树](device-tree.md)

[硬件资源](hardware-resources.md)

[PnP 设备的状态转换](state-transitions-for-pnp-devices.md)

 

