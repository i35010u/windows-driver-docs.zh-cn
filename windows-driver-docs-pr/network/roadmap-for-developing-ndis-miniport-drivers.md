---
title: NDIS 微型端口驱动程序开发路线图
description: NDIS 微型端口驱动程序开发路线图
ms.assetid: 7cb56c08-3578-49d7-a0aa-a89dc6b139ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4524f11bed854352543f2a69e6252404f18a8430
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842011"
---
# <a name="roadmap-for-developing-ndis-miniport-drivers"></a>NDIS 微型端口驱动程序开发路线图


若要创建网络驱动程序接口规范（NDIS）微型端口驱动程序包，请执行以下步骤：

- 步骤1：了解 Windows 体系结构和驱动程序。

  您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅[所有驱动程序开发人员的概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)。

- 步骤2：了解 NDIS。

  有关 NDIS 和 NDIS 驱动程序的常规信息，请参阅以下主题：

  [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

  [网络驱动程序编程注意事项](network-driver-programming-considerations.md)

  [驱动程序堆栈管理](driver-stack-management.md)

  [NET\_缓冲器体系结构](net-buffer-architecture.md)

- 步骤3：确定其他 Windows 驱动程序设计决策。

  有关如何进行其他 Windows 设计决策的详细信息，请参阅[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)、 [64 位驱动程序的编程问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)以及[创建国际 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

- 步骤4：了解 Windows 驱动程序的生成、测试和调试过程和工具。

  构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和[Windows 硬件认证工具包（HCK）](https://go.microsoft.com/fwlink/p/?LinkId=733613)测试的详细信息，请参阅[生成、调试和测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 有关生成、测试、验证和调试工具的详细信息，请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)。

- 步骤5：阅读微型端口驱动程序简介主题。
  
  [网络接口卡](network-interface-card-support.md)的[NDIS 微型端口驱动程序的类型](types-of-ndis-miniport-drivers.md)
  [微型端口驱动程序代码的重要功能](important-features-of-miniport-driver-code.md)
  [示例 NDIS 微型端口驱动程序](sample-ndis-miniport-drivers.md)
- 步骤6：阅读[写入微型端口驱动程序部分](writing-ndis-miniport-drivers.md)。

  本部分概述了主要微型端口驱动程序接口。 这些接口包括微型端口驱动程序提供的函数（*MiniportXxx*函数）和用于启动操作的 NDIS 调用。 NDIS 为**ndis * Xxx*** 函数提供了微型端口驱动程序调用来执行 Ndis 操作的函数。

- 步骤7：查看 GitHub 上[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[NDIS 微型端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918)。

- 步骤8：（可选阅读）微型端口驱动程序的其他注意事项。

  其他注意事项包括扩展[微型端口驱动程序部分](writing-ndis-miniport-drivers.md)中所述的主要接口的主题。

  [获取和设置微型端口驱动程序信息和 WMI 对 WMI 的支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)

  [NDIS MSI-X](ndis-msi-x.md)

  [NDIS 散播/聚集 DMA](ndis-scatter-gather-dma.md)

  [NDIS 电源管理](ndis-power-management.md)

  [用于 NDIS 微型端口驱动程序的即插即用](plug-and-play-for-ndis-miniport-drivers.md)

  [重置、停止和关闭函数](reset--halt--and-shutdown-functions.md)

  [具有 WDM 下接口的微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/miniport-drivers-with-a-wdm-lower-interface)

  [WAN 微型端口驱动程序](wan-miniport-drivers.md)

  [可缩放网络](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

- 步骤9：开发（或端口）、构建、测试和调试 NDIS 驱动程序。

  如果要移植现有驱动程序，请参阅移植指南：

  -   [将 NDIS 1.x 驱动程序移植到 NDIS 6。0](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [将 NDIS 1.x 驱动程序移植到 NDIS 6.20](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [将 NDIS 1.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  有关迭代生成、测试和调试的详细信息，请参阅[生成、调试和测试过程的概述](https://docs.microsoft.com/windows-hardware/drivers)。 此过程有助于确保构建一个可正常工作的驱动程序。

- 步骤10：为驱动程序创建驱动程序包。

  有关如何安装驱动程序的详细信息，请参阅[提供驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。 有关如何安装 NDIS 驱动程序的详细信息，请参阅[安装和升级网络组件](installing-and-upgrading-network-components.md)。

- 步骤11：对驱动程序进行签名和分发。

  最后一步是对驱动程序进行签名（可选）和分发。 如果你的驱动程序满足为[Windows 硬件认证包（HCK）](https://go.microsoft.com/fwlink/p/?LinkId=733613)定义的质量标准，你可以通过 Microsoft Windows 更新计划分发它。 有关如何分发驱动程序的详细信息，请参阅[分发驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。

 

 





