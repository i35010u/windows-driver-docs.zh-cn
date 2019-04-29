---
title: 使用 Winsock 内核的网络驱动程序开发路线图
description: 使用 Winsock 内核的网络驱动程序开发路线图
ms.assetid: f94952c3-02b1-4bd2-bd73-e6d6d42a06fb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e4c42e9936fb4f948af432bf9d5803f9b7e5cc6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359415"
---
# <a name="roadmap-for-developing-network-drivers-with-winsock-kernel"></a>使用 Winsock 内核的网络驱动程序开发路线图


若要创建使用内核模式套接字编程功能的 Winsock Kernel (WSK) 的网络驱动程序包，请执行以下步骤：

-   **步骤 1:** 了解 Windows 体系结构和驱动程序。

    你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助你做出适当的设计决策，还可以简化开发过程。 有关驱动程序的基本原理的详细信息，请参阅[的所有驱动程序开发人员概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)。

-   **步骤 2:** 了解有关网络驱动程序接口规格 (NDIS)。

    驱动程序包通常会使用网络驱动程序接口规范 (NDIS) 接口。 有关详细信息，有关 NDIS 和 NDIS 微型端口驱动程序，请参阅以下主题：

    [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

    [NDIS 微型端口驱动程序](ndis-miniport-drivers.md)

    [编写 NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)

    [网络驱动程序的编程注意事项](network-driver-programming-considerations.md)

-   **步骤 3：** 确定要在您的驱动程序中使用的其他网络组件。

    除了核心 NDIS 功能，可以使用内核模式驱动程序，具体取决于硬件配置以下附加 Windows 网络组件：

    [IP 帮助程序](ip-helper.md)

    [Windows 筛选平台标注驱动程序](introduction-to-windows-filtering-platform-callout-drivers.md)

    [本机 802.11 无线 LAN](https://msdn.microsoft.com/library/windows/hardware/ff560689)

    [移动宽带网络接口](mb-interface-overview.md)

-   **步骤 4：** 了解 Winsock 内核的基础知识。

    在 Windows Vista 和更高版本的 Windows 支持 Winsock 内核。 有关如何使用 Winsock 内核的信息，请参阅[简介 Winsock 内核](introduction-to-winsock-kernel.md)。

    一个更简单、 更通用的网络编程接口，您可以使用网络驱动程序中是[网络模块注册机构](network-module-registrar2.md)。

-   **步骤 5:** 确定其他 Windows 驱动程序的设计决策。

    有关如何使更多 Windows 设计决策，请参阅[创建可靠的内核模式驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff542904)，[的 64 位驱动程序的编程问题](https://msdn.microsoft.com/library/windows/hardware/ff559923)，和[创建国际 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff540208)。

-   **步骤 6：** 了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

    构建一个驱动程序不同于生成在用户模式应用程序。 有关 Windows 驱动程序生成、 调试和测试过程，驱动程序签名，并[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)测试，请参阅[构建、 调试和测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。 了解工具来构建、 测试、 验证和调试，请参阅[驱动程序开发工具](https://msdn.microsoft.com/library/windows/hardware/ff545440)。

-   **步骤 7:** 审阅[Winsock Kernel （WSK TCP Echo 服务器） 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617935)中[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

-   **步骤 8:** 开发、 生成、 测试和调试您的驱动程序。

    有关迭代构建、 测试和调试的信息，请参阅[概述的构建、 调试和测试过程](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。 此过程有助于确保您构建适用的驱动程序。

-   **步骤 9:** 创建您的驱动程序的驱动程序包。

    有关如何安装驱动程序的信息，请参阅[提供一个驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)。

-   **步骤 10:** 签名和分发您的驱动程序。

    最后一步是登录 （可选） 和分发该驱动程序。 如果您的驱动程序符合质量标准，为定义[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)，可以将其分配通过 Microsoft Windows 更新计划。 有关如何将驱动程序分发的详细信息，请参阅[分发驱动程序](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 





