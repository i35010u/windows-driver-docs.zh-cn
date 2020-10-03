---
title: NDIS 微型端口驱动程序开发路线图
description: NDIS 微型端口驱动程序开发路线图
ms.assetid: 7cb56c08-3578-49d7-a0aa-a89dc6b139ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f63b8a94048ce66db19bd1e3ebbb8d1dd28d353b
ms.sourcegitcommit: 29fee075ccc0a4eb1bf304cca4c04a6e57449d9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91671233"
---
# <a name="roadmap-for-developing-ndis-miniport-drivers"></a>NDIS 微型端口驱动程序开发路线图

若要创建网络驱动程序接口规范 (NDIS) 微型端口驱动程序包，请执行以下步骤：

- 步骤1：了解 Windows 体系结构和驱动程序。

  您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

- 步骤2：了解 NDIS。

  有关 NDIS 和 NDIS 驱动程序的常规信息，请参阅以下主题：

  [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

  [网络驱动程序编程注意事项](network-driver-programming-considerations.md)

  [驱动程序堆栈管理](driver-stack-management.md)

  [网络 \_ 缓冲区体系结构](net-buffer-architecture.md)

- 步骤3：确定其他 Windows 驱动程序设计决策。

  有关如何进行其他 Windows 设计决策的详细信息，请参阅 [创建可靠的内核模式驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)、 [64 位驱动程序的编程问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)以及 [创建国际 INF 文件](../install/creating-international-inf-files.md)。

- 步骤4：了解 Windows 驱动程序的生成、测试和调试过程和工具。

  构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 测试的详细信息，请参阅 [生成、调试和测试驱动程序](/windows-hardware/drivers)。 有关生成、测试、验证和调试工具的详细信息，请参阅 [驱动程序开发工具](../devtest/index.md)。

- 步骤5：阅读微型端口驱动程序简介主题。
  [NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md) 
   的类型[网络接口卡支持](network-interface-card-support.md) 
  [示例 NDIS 微型端口驱动程序](sample-ndis-miniport-drivers.md)
- 步骤6：阅读 [写入微型端口驱动程序部分](./initializing-a-miniport-driver.md)。

  本部分概述了主要微型端口驱动程序接口。 这些接口包含了微型端口驱动程序提供 (*MiniportXxx* 函数的函数) 和 NDIS 调用来启动操作。 NDIS 为 **ndis * Xxx*** 函数提供了微型端口驱动程序调用来执行 Ndis 操作的函数。

- 步骤7：查看 GitHub 上[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[NDIS 微型端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918)。

- 步骤8： (可选阅读) 微型端口驱动程序的其他注意事项。

  其他注意事项包括扩展 [微型端口驱动程序部分](./initializing-a-miniport-driver.md)中所述的主要接口的主题。

  [获取和设置 WMI 的微型端口驱动程序信息与 NDIS 支持](ndis-management-information-and-oids.md)

  [NDIS MSI-X](ndis-msi-x.md)

  [NDIS 分散/聚合 DMA](ndis-scatter-gather-dma.md)

  [NDIS 电源管理](power-management--ndis-6-30-.md)

  [NDIS 微型端口驱动程序的即插即用](exporting-a-miniportdevicepnpeventnotify-function.md)

  [重置、停止和关闭函数](hardware-reset.md)

  [具有 WDM 下接口的微型端口驱动程序](./miniport-drivers-with-a-wdm-lower-interface.md)

  [WAN 微型端口驱动程序](wan-miniport-drivers.md)

  [可缩放网络](/windows-hardware/drivers/ddi/_netvista/)

- 步骤9：开发 (或端口) 、构建、测试和调试 NDIS 驱动程序。

  如果要移植现有驱动程序，请参阅移植指南：

  - [将 NDIS 1.x 驱动程序移植到 NDIS 6。0](/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  - [将 NDIS 6.x 驱动程序移植到 NDIS 6.20](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  - [将 NDIS 6.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  有关迭代生成、测试和调试的详细信息，请参阅 [生成、调试和测试过程的概述](/windows-hardware/drivers)。 此过程有助于确保构建一个可正常工作的驱动程序。

- 步骤10：为驱动程序创建驱动程序包。

  有关如何安装驱动程序的详细信息，请参阅 [提供驱动程序包](/windows-hardware/drivers)。 有关如何安装 NDIS 驱动程序的详细信息，请参阅 [用于安装网络组件的组件和文件](components-and-files-used-for-network-component-installation.md) 和 [通知网络组件对象](notify-objects-for-network-components.md)。

- 步骤11：对驱动程序进行签名和分发。

  最后一步是对 (可选) 进行签名，然后分发驱动程序。 如果你的驱动程序满足为 [Windows 硬件认证工具包 ](https://go.microsoft.com/fwlink/p/?LinkId=733613)定义的质量标准 (HCK) ，你可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关如何分发驱动程序的详细信息，请参阅 [分发驱动程序](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。
