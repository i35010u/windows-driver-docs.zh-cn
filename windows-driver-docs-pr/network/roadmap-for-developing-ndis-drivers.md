---
title: NDIS 驱动程序开发路线图
description: NDIS 驱动程序开发路线图
ms.assetid: 4adc5438-d2ea-4b05-bbf3-e86cc5f3105a
keywords:
- NDIS WDK，驱动程序
- NDIS WDK，驱动程序，开发
- 开发 NDIS 驱动程序 WDK
- " (NDIS) WDK 的网络驱动程序接口规范"
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74c19973f4cd111107cb5df90aa65142c22fd2d8
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734254"
---
# <a name="roadmap-for-developing-ndis-drivers"></a>NDIS 驱动程序开发路线图

若要创建网络驱动程序接口规范 (NDIS) 驱动程序包，请执行以下步骤：

- 步骤1：了解 Windows 体系结构和驱动程序。

    您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

- 步骤2：了解 NDIS。

    有关 NDIS 和 NDIS 驱动程序的常规信息，请参阅以下主题：

    [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

    [网络驱动程序编程注意事项](network-driver-programming-considerations.md)

    [驱动程序堆栈管理](driver-stack-management.md)

    [网络 \_ 缓冲区体系结构](net-buffer-architecture.md)

- 步骤3：确定其他 Windows 驱动程序设计决策。

    有关如何进行其他 Windows 设计决策的详细信息，请参阅 [创建可靠的内核模式驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)、 [64 位驱动程序的编程问题](../kernel/porting-your-driver-to-64-bit-windows.md)以及 [创建国际 INF 文件](../install/creating-international-inf-files.md)。

- 步骤4：了解 Windows 驱动程序的生成、测试和调试过程和工具。

    构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 测试的详细信息，请参阅 [生成、调试和测试驱动程序](/windows-hardware/drivers)。 有关生成、测试、验证和调试工具的详细信息，请参阅 [驱动程序开发工具](../devtest/index.md)。

- 步骤5：选择要实现的 NDIS 驱动程序的类型。

    有关 NDIS 驱动程序类型的详细信息，请参阅 [使用网络驱动程序设计指南](using-the-network-driver-design-guide.md)。

    遵循驱动程序类型的路线图。

    [NDIS 微型端口驱动程序开发路线图](roadmap-for-developing-ndis-miniport-drivers.md)

    [NDIS 协议驱动程序的开发路线图](roadmap-for-developing-ndis-protocol-drivers.md)

    [NDIS 筛选器驱动程序开发路线图](roadmap-for-developing-ndis-filter-drivers.md)

    [NDIS 中间驱动程序的开发路线图](roadmap-for-developing-ndis-intermediate-drivers.md)

    [开发移动宽带微型端口驱动程序的路线图](roadmap-to-develop-mb-miniport-drivers.md)

    [开发 Windows 筛选平台标注驱动程序的路线图](roadmap-for-developing-wfp-callout-drivers.md)

- 步骤6：查看 GitHub 上[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[网络驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616034)。

- 步骤7：开发 (或端口) 、构建、测试和调试 NDIS 驱动程序。

    如果要移植现有驱动程序，请参阅移植指南：

  - [将 NDIS 6.x 驱动程序移植到 NDIS 6.40](porting-ndis-6-x-drivers-to-ndis-6-40.md)
  - [将 NDIS 6.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)
  - [将 NDIS 6.x 驱动程序移植到 NDIS 6.20](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  - [将 NDIS 1.x 驱动程序移植到 NDIS 6。0](/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)

    有关迭代生成、测试和调试的详细信息，请参阅 [生成、调试和测试过程的概述](/windows-hardware/drivers)。 此过程有助于确保构建一个可正常工作的驱动程序。

- 步骤8：为驱动程序创建驱动程序包。

    有关如何安装驱动程序的详细信息，请参阅 [提供驱动程序包](/windows-hardware/drivers)。 有关如何安装 NDIS 驱动程序的详细信息，请参阅 [用于安装网络组件的组件和文件](components-and-files-used-for-network-component-installation.md) 和 [通知网络组件对象](notify-objects-for-network-components.md)。

- 步骤9：对驱动程序进行签名和分发。

    最后一步是对驱动程序进行签名和分发。 如果你的驱动程序满足为 [Windows 硬件认证工具包 ](https://go.microsoft.com/fwlink/p/?LinkId=733613)定义的质量标准 (HCK) ，你可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关如何分发驱动程序的详细信息，请参阅 [分发驱动程序](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。