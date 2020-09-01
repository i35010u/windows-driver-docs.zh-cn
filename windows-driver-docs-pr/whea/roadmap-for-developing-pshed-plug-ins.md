---
title: 用于开发 PSHED 插件的路线图
description: 用于开发 PSHED 插件的路线图
ms.assetid: 3e1eb744-e480-4478-9705-94da8029c382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f43c5d300d3f7583b90ad9fd4d282d51ef5c6312
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208399"
---
# <a name="roadmap-for-developing-pshed-plug-ins"></a>用于开发 PSHED 插件的路线图


![指向地图的罗盘、地图和手指的插图](images/map-hand-sml.png)

平台特定的硬件错误驱动程序 (PSHED) 是 Windows 硬件错误体系结构的一个组件，用于收集特定于平台的错误信息 (WHEA) 。 PSHED 提供了一个抽象层，此层高于底层平台的硬件错误报告功能，通过提供此层，PSHED 将从操作系统中隐藏平台错误处理功能的详细信息，并向 Windows 操作系统公开一致性错误处理接口。

在涉及系统固件接口到硬件错误处理资源的平台上，PSHED 管理与固件的接口。 它通过使用由平台供应商实现的 PSHED 插件来实现此功能。

PSHED 插件是基于 Windows 驱动程序模型 (WDM) 的驱动程序，它提供了硬件平台错误报告和恢复功能的软件接口。

PSHED 插件还可以通过使用平台供应商定义的专用接口，与平台固件交互。 这允许平台供应商继续使用现有固件进行硬件错误处理。

若要为 Windows Vista 和更高版本的 Windows 创建 PSHED 插件驱动程序，请执行以下步骤：

-   步骤1：了解 Windows 体系结构和驱动程序。

    首先，必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。

    有关驱动程序基础的详细信息，请参阅 [了解驱动程序和操作系统基础知识](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

-   步骤2：了解 Windows 硬件错误体系结构的基础知识 (WHEA) 。

    WHEA 是随 Windows Vista 一起引入的，它扩展了以前版本的 Windows 的硬件错误报告功能，并将这些机制作为相关硬件错误基础结构的组件一起提供。 WHEA 使用当今硬件设备中提供的其他硬件错误信息，并与系统固件紧密集成。

    您必须了解 Windows Vista 和更高版本的 Windows 中的 WHEA 的基础知识。 这将帮助你了解 WHEA 的功能组件，这些组件也可帮助你做出适当的设计决策。

    有关 WHEA 的详细信息，请参阅 [Windows 硬件错误体系结构简介](introduction-to-the-windows-hardware-error-architecture.md) 和 [Windows 硬件错误体系结构概述](windows-hardware-error-architecture-overview.md)。

-   步骤3：了解 Windows 驱动程序的生成、测试和调试过程和工具。

    构建驱动程序与构建用户模式应用程序不同。

    有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 Windows 徽标测试的信息，请参阅 [生成、调试和测试驱动程序](/windows-hardware/drivers)。

    有关生成、测试、验证和调试工具的信息，请参阅 [驱动程序开发工具](../devtest/index.md)。

-   步骤4：作出有关 PSHED 插件的设计决策。

    开始设计 PSHED 插件之前，必须先了解以下内容：

    -   Windows Vista 和更高版本的 Windows 的 PSHED 插件的功能要求和操作。

        有关详细信息，请参阅[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

    -   自 Windows Vista 以来对 WHEA 所做的更改。

        有关这些更改的详细信息，请参阅 [Windows 硬件错误体系结构的新信息](new-information-for-windows-hardware-error-architecture.md)。

-   步骤5：开发、构建、测试和调试 PSHED 插件。

    以下主题中的信息将帮助你生成可正常工作的 PSHED 插件：

    -   有关开发 PSHED 插件的指导原则，请参阅 [PSHED 插件指南](pshed-plug-in-guidelines.md)。
    -   有关如何生成 PSHED 插件的信息，请参阅 [生成 PSHED 插件](building-a-pshed-plug-in.md)。
    -   有关可用于调试 PSHED 插件的 WHEA 调试器扩展的信息，请参阅 [Windows 硬件错误体系结构调试器扩展](windows-hardware-error-architecture-debugger-extensions.md)。
    -   有关迭代生成、测试和调试的信息，请参阅 [生成、调试和测试过程的概述](/windows-hardware/drivers)。
-   步骤6：为 PSHED 插件创建驱动程序包。

    PSHED 插件是 WDM 驱动程序。 与其他 WDM 驱动程序一样，PSHED 插件是使用 [驱动程序包](../install/driver-packages.md)安装的。

    有关驱动程序包的详细信息，请参阅 [提供驱动程序包](/windows-hardware/drivers)。

    有关如何安装 PSHED 插件的驱动程序包的详细信息，请参阅 [PSHED 插件安装](pshed-plug-in-installation.md)。

-   步骤7：签署和分发 PSHED 插件。

    最后一步是对 PSHED 插件进行数字签名和分发。 PSHED 的插件不适合任何现有的 Windows 硬件质量实验室 (WHQL) 测试程序。 因此，PSHED 插件必须使用 Authenticode 签名进行数字签名。

    有关签名和分发 PSHED 插件的详细信息，请参阅 [限定和分发 PSHED 插件](qualifying-and-distributing-pshed-plug-ins.md)。

这些是基本步骤。 根据单个 PSHED 插件的需要，可能需要执行其他步骤。

 

