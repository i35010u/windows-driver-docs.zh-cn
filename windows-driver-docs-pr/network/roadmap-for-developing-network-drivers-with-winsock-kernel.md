---
title: 使用 Winsock 内核的网络驱动程序开发路线图
description: 使用 Winsock 内核的网络驱动程序开发路线图
ms.assetid: f94952c3-02b1-4bd2-bd73-e6d6d42a06fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b7501dc410c9f61e895919937ee661a21bd4ebd
ms.sourcegitcommit: 20eac54e419a594f7cea766ee28f158559dfd79c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91754988"
---
# <a name="roadmap-for-developing-network-drivers-with-winsock-kernel"></a>使用 Winsock 内核的网络驱动程序开发路线图


若要创建使用 Winsock 内核 (WSK) 的内核模式套接字编程功能的网络驱动程序包，请执行以下步骤：

-   **步骤1：** 了解 Windows 体系结构和驱动程序。

    您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

-   **步骤2：** (NDIS) 了解网络驱动程序接口规范。

    驱动程序包通常使用 (NDIS) 接口的网络驱动程序接口规范。 有关 NDIS 和 NDIS 微型端口驱动程序的详细信息，请参阅以下主题：

    [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

    [NDIS 微型端口驱动程序](roadmap-for-developing-ndis-miniport-drivers.md)

    [编写 NDIS 微型端口驱动程序](./initializing-a-miniport-driver.md)

    [网络驱动程序编程注意事项](network-driver-programming-considerations.md)

-   **步骤3：** 确定要在驱动程序中使用的其他网络组件。

    除核心 NDIS 功能外，还可以将以下附加 Windows 网络组件用于内核模式驱动程序，具体取决于硬件配置：

    [IP 帮助程序](ip-helper.md)

    [Windows 筛选平台标注驱动程序](introduction-to-windows-filtering-platform-callout-drivers.md)

    [本机802.11 无线 LAN](/previous-versions/windows/hardware/wireless/ff560689(v=vs.85))

    [移动宽带网络接口](mb-interface-overview.md)

-   **步骤4：** 了解 Winsock 内核的基本知识。

    Windows Vista 和更高版本的 Windows 支持 Winsock 内核。 有关如何使用 Winsock 内核的信息，请参阅 [Winsock 内核简介](introduction-to-winsock-kernel.md)。

    网络驱动程序中可以使用的更简单、更通用的网络编程接口是 [网络模块注册](network-module-registrar2.md)器。

-   **步骤5：** 确定其他 Windows 驱动程序设计决策。

    有关如何进行其他 Windows 设计决策的信息，请参阅 [创建可靠的内核模式驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)、 [64 位驱动程序的编程问题](../kernel/porting-your-driver-to-64-bit-windows.md)以及 [创建国际 INF 文件](../install/creating-international-inf-files.md)。

-   **步骤6：** 了解 Windows 驱动程序的生成、测试和调试过程和工具。

    构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 测试的信息，请参阅 [生成、调试和测试驱动程序](/windows-hardware/drivers)。 有关用于生成、测试、验证和调试的工具的信息，请参阅 [驱动程序开发工具](../devtest/index.md)。

-   **步骤7：** 查看 GitHub 上的[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[WINSOCK 内核 (WSK TCP Echo Server) 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617935)。

-   **步骤8：** 开发、构建、测试和调试驱动程序。

    有关迭代生成、测试和调试的信息，请参阅 [生成、调试和测试过程的概述](/windows-hardware/drivers)。 此过程有助于确保你构建的驱动程序有效。

-   **步骤9：** 为驱动程序创建驱动程序包。

    有关如何安装驱动程序的信息，请参阅 [提供驱动程序包](/windows-hardware/drivers)。

-   **步骤10：** 签署和分发您的驱动程序。

    最后一步是对 (可选) 进行签名，然后分发驱动程序。 如果你的驱动程序满足为 [Windows 硬件认证工具包 ](https://go.microsoft.com/fwlink/p/?LinkId=733613)定义的质量标准 (HCK) ，你可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关如何分发驱动程序的详细信息，请参阅 [分发驱动程序](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。

