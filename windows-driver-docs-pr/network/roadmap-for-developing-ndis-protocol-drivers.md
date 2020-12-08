---
title: NDIS 协议驱动程序的开发路线图
description: NDIS 协议驱动程序的开发路线图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15f0dad63b2fdd68651e1048a5a08251ba2a8efb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789635"
---
# <a name="roadmap-for-developing-ndis-protocol-drivers"></a>NDIS 协议驱动程序的开发路线图

若要创建网络驱动程序接口规范 (NDIS) 协议驱动程序包，请执行以下步骤：

- 步骤1：了解 Windows 体系结构和驱动程序。

  您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

- 步骤2：了解 NDIS。

  有关 NDIS 和 NDIS 驱动程序的常规信息，请参阅以下主题：

  [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

  [网络驱动程序编程注意事项](network-driver-programming-considerations.md)

  [驱动程序堆栈管理](driver-stack-management.md)

  [网络 \_ 缓冲区体系结构](net-buffer-architecture.md)

- 步骤3：确定其他 Windows 驱动程序设计决策。

  有关如何进行其他 Windows 设计决策的详细信息，请参阅 [创建可靠 Kernel-Mode 驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)、 [64 位驱动程序的编程问题](../kernel/porting-your-driver-to-64-bit-windows.md)以及 [创建国际 INF 文件](../install/creating-international-inf-files.md)。

- 步骤4：了解 Windows 驱动程序的生成、测试和调试过程和工具。

  构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 测试的详细信息，请参阅 [生成、调试和测试驱动程序](/windows-hardware/drivers)。 有关生成、测试、验证和调试工具的详细信息，请参阅 [驱动程序开发工具](../devtest/index.md)。

- 步骤5：阅读协议驱动程序简介主题。
  [NDIS 协议驱动程序简介](introduction-to-ndis-protocol-drivers.md) 
  [协议驱动程序设计概念](pageable-and-discardable-code-in-a-protocol-driver.md)
- 步骤6：阅读 [编写协议驱动程序部分](initializing-a-protocol-driver.md)。

  本部分概述了主要协议驱动程序接口。 这些接口包含协议驱动程序提供 (*ProtocolXxx* 函数的函数) 和 NDIS 调用来启动操作。 NDIS 提供 **ndis * Xxx*** 函数，这些函数用于执行 ndis 操作的协议驱动程序调用。

- 步骤7：查看 GitHub 上[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[NDIS 协议驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617917)。

- 步骤8：开发 (或端口) 、构建、测试和调试 NDIS 驱动程序。

  如果要移植现有驱动程序，请参阅移植指南：

  - [将 NDIS 1.x 驱动程序移植到 NDIS 6。0](/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  - [将 NDIS 6.x 驱动程序移植到 NDIS 6.20](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  - [将 NDIS 6.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  有关迭代生成、测试和调试的详细信息，请参阅 [生成、调试和测试过程的概述](/windows-hardware/drivers)。 此过程有助于确保构建一个可正常工作的驱动程序。

- 步骤9：为驱动程序创建驱动程序包。

  有关如何安装驱动程序的详细信息，请参阅 [提供驱动程序包](/windows-hardware/drivers)。 有关如何安装 NDIS 驱动程序的详细信息，请参阅 [用于安装网络组件的组件和文件](components-and-files-used-for-network-component-installation.md) 和 [通知网络组件对象](notify-objects-for-network-components.md)。

- 步骤10：对驱动程序进行签名和分发。

  最后一步是对 (可选) 进行签名，然后分发驱动程序。 如果你的驱动程序满足为 [Windows 硬件认证工具包 ](https://go.microsoft.com/fwlink/p/?LinkId=733613)定义的质量标准 (HCK) ，你可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关如何分发驱动程序的详细信息，请参阅 [分发驱动程序](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。
