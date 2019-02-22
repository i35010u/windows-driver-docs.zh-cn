---
title: 用于开发 PSHED 插件的路线图
description: 用于开发 PSHED 插件的路线图
ms.assetid: 3e1eb744-e480-4478-9705-94da8029c382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b59a3972ad9a9e09a08da880ace307e68d096f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555247"
---
# <a name="roadmap-for-developing-pshed-plug-ins"></a>用于开发 PSHED 插件的路线图


![示意图，指南针，一个映射，以及指向映射手指](images/map-hand-sml.png)

特定于平台的硬件错误驱动程序 (PSHED) 是一个组件的 Windows 硬件错误体系结构 (WHEA) 用来收集特定于平台的错误信息。 PSHED 通过提供这一层提供上面基础平台的硬件错误报告功能的抽象层、 PSHED 隐藏某个平台的错误处理来自操作系统的功能的详细信息，并公开一致的错误处理对 Windows 操作系统的接口。

在涉及到硬件错误处理资源的系统固件接口的平台，PSHED 管理固件的接口。 通过使用由平台供应商实现 PSHED 插件执行此操作。

PSHED 插件是基于 Windows 驱动程序模型 (WDM)，并提供了错误的软件界面的硬件平台的报告和恢复功能的驱动程序。

PSHED 插件还可与平台固件使用由平台供应商定义的专用接口。 这样，平台供应商联系以继续使用现有的固件硬件错误处理。

若要创建适用于 Windows Vista 和更高版本的 Windows PSHED 插件驱动程序，请执行以下步骤：

-   第 1 步：了解 Windows 体系结构和驱动程序。

    您必须首先了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助你做出适当的设计决策，还可以简化开发过程。

    有关驱动程序的基本原理的详细信息，请参阅[了解驱动程序和操作系统的基础知识](https://msdn.microsoft.com/library/windows/hardware/ff554731)。

-   步骤 2：了解基础知识的 Windows 硬件错误体系结构 (WHEA)。

    WHEA，引入了 Windows Vista，扩展的 Windows，以前的版本的硬件错误报告功能，并将这些机制结合在一起以一致的硬件错误基础结构的组件。 WHEA 使用额外的硬件错误信息，可在今天的硬件设备，并与系统固件得更紧密地集成。

    您必须了解的 Windows Vista 中的 WHEA 基础知识以及更高版本的 Windows。 这将帮助你了解 WHEA，还将帮助你做出适当的设计决策的功能组件。

    WHEA 的详细信息，请参阅[Windows 硬件错误体系结构简介](introduction-to-the-windows-hardware-error-architecture.md)并[Windows 硬件错误体系结构概述](windows-hardware-error-architecture-overview.md)。

-   步骤 3:了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

    构建一个驱动程序不是与构建在用户模式应用程序相同。

    有关 Windows 驱动程序生成、 调试和测试过程，驱动程序签名，和 Windows 徽标测试的信息，请参阅[构建、 调试和测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。

    了解有关生成，测试、 验证和调试工具，请参阅[驱动程序开发工具](https://msdn.microsoft.com/library/windows/hardware/ff545440)。

-   步骤 4：请设计决策有关你 PSHED 插件。

    在开始您 PSHED 插件设计之前，首先必须了解以下：

    -   功能性要求和操作的 PSHED 插件适用于 Windows Vista 和更高版本的 Windows。

        有关详细信息，请参阅[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

    -   已推出 Windows Vista 对 WHEA 的更改。

        有关这些更改的详细信息，请参阅[新信息的 Windows 硬件错误体系结构](new-information-for-windows-hardware-error-architecture.md)。

-   步骤 5：开发、 构建、 测试和调试你 PSHED 插件。

    以下主题中的信息将帮助您正确生成 PSHED 插件有效的：

    -   有关开发 PSHED 插件的指南，请参阅[PSHED 插件准则](pshed-plug-in-guidelines.md)。
    -   有关如何生成 PSHED 插件的信息，请参阅[构建 PSHED 插件](building-a-pshed-plug-in.md)。
    -   有关可用于调试 PSHED 插件的 WHEA 调试器扩展的信息，请参阅[Windows 硬件错误体系结构调试器扩展](windows-hardware-error-architecture-debugger-extensions.md)。
    -   有关迭代构建、 测试和调试的信息，请参阅[概述的构建、 调试和测试过程](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。
-   步骤 6：驱动程序包为创建你 PSHED 插件。

    PSHED 插件是一个 WDM 驱动程序。 与其他 WDM 驱动程序，PSHED 插件安装后通过使用[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)。

    有关驱动程序包的详细信息，请参阅[提供一个驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)。

    有关如何为 PSHED 插件安装驱动程序包的详细信息，请参阅[PSHED 插件安装](pshed-plug-in-installation.md)。

-   步骤 7：签名并分发你 PSHED 插件。

    最后一步是进行数字签名并分发你 PSHED 插件。 PSHED 插件不适合的任何现有的 Windows 硬件质量实验室 (WHQL) 测试计划。 因此，必须通过使用验证码签名进行数字签名 PSHED 插件。

    有关签名和分发您 PSHED 插件的详细信息，请参阅[资格和分发 PSHED 插件](qualifying-and-distributing-pshed-plug-ins.md)。

这些是基本步骤。 根据需要在单个 PSHED 插件可能有必要执行其他步骤。

 

 




