---
title: 即插即用简介
description: 即插即用简介
keywords:
- PnP WDK 内核，关于即插即用
- 即插即用 WDK 内核，关于即插即用
ms.date: 03/10/2021
ms.localizationpriority: medium
ms.custom: contperf-fy21q3
ms.openlocfilehash: 1aa5136a7677424c283cbfd9e25419fb79cb08fa
ms.sourcegitcommit: 47cd14eb928aee3a3368d9d1d92a7047b30eac55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/11/2021
ms.locfileid: "103022574"
---
# <a name="introduction-to-plug-and-play"></a>即插即用简介

本部分包含以下其他主题：

[PnP 组件](pnp-components.md)

[PnP 驱动程序设计指导原则](pnp-driver-design-guidelines.md)

[硬件资源](hardware-resources.md)

即插即用 (PnP) 是 Windows 的一部分，它使计算机系统能够通过用户的最小干预来适应硬件更改。 用户无需手动配置即可添加和删除设备，也无需了解计算机硬件。 例如，用户可以在不进行手动配置更改的情况下，插接便携式计算机并使用插接站键盘、鼠标和监视器。

PnP 需要设备硬件、系统软件和驱动程序的支持。 硬件行业中的方案定义了用于轻松识别外接板和系统组件的标准。 此 Windows 驱动程序工具包 (WDK) 文档重点介绍适用于 PnP 的系统软件支持以及驱动程序如何使用该支持来实现 PnP。

PnP 的系统软件支持与 PnP 驱动程序一起提供以下内容：

-   自动和动态识别已安装的硬件

-   硬件资源分配 (和重新分配) 

    PnP 管理器会确定每个设备请求的硬件资源 (例如，输入/输出端口、中断请求、直接内存访问通道和内存位置) 并相应地分配硬件资源。 必要时，PnP 管理器会重新配置资源分配，如将新设备添加到需要已使用资源的系统时。

    PnP 设备的驱动程序不分配资源;而是在枚举设备时标识设备的请求资源。 PnP 管理器检索资源分配过程中每个设备的要求。 对于旧设备，无法动态配置资源，因此 PnP 管理器首先将资源分配给旧设备。

-   加载相应的驱动程序

-   用于与 PnP 系统交互的驱动程序的编程接口

    该接口包含 i/o 管理器例程，即插即用次 Irp，必需的 [标准驱动程序例程](./introduction-to-standard-driver-routines.md)，以及注册表中的信息。

-   驱动程序和应用程序用于了解硬件环境中的变化并采取适当措施的机制

    PnP 允许驱动程序和用户模式代码注册特定硬件事件并向其发送通知。

要使驱动程序符合 PnP 要求，必须提供所需的 PnP 入口点，处理所需的 PnP Irp，并遵循 PnP 指导原则。
