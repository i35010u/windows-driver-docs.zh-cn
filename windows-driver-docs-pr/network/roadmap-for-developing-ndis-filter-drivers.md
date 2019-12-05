---
title: NDIS 筛选器驱动程序开发路线图
description: NDIS 筛选器驱动程序开发路线图
ms.assetid: 346dae93-4cb7-4cb5-a2cf-41be9809fec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0abc1e52ab5c874ec4a552446718e5ad6e39e231
ms.sourcegitcommit: b7971067b64ffa9162bfedc263ce4de53dcbe9b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74832874"
---
# <a name="roadmap-for-developing-ndis-filter-drivers"></a>NDIS 筛选器驱动程序开发路线图


若要创建网络驱动程序接口规范（NDIS）筛选器驱动程序包，请执行以下步骤：

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

  构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和[Windows 硬件兼容性](https://docs.microsoft.com/windows-hardware/design/compatibility/)测试的详细信息，请参阅[生成、调试和测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 有关生成、测试、验证和调试工具的详细信息，请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)。

- 步骤5：阅读[筛选器驱动程序简介主题](introduction-to-ndis-filter-drivers.md)。

- 步骤6：阅读[编写协议驱动程序部分](writing-ndis-miniport-drivers.md)。

  本部分概述了主要协议驱动程序接口。 这些接口包含协议驱动程序提供的函数（*ProtocolXxx*函数）和用于启动操作的 NDIS 调用。 NDIS 提供**ndis * Xxx*** 函数，这些函数用于执行 ndis 操作的协议驱动程序调用。

- 步骤7：查看 GitHub 上的[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[NDIS 筛选器驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617915)。

- 步骤8：开发（或端口）、构建、测试和调试 NDIS 驱动程序。

  如果要移植现有驱动程序，请参阅移植指南：

  -   [将 NDIS 1.x 驱动程序移植到 NDIS 6。0](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [将 NDIS 1.x 驱动程序移植到 NDIS 6.20](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [将 NDIS 1.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  有关迭代生成、测试和调试的详细信息，请参阅[生成、调试和测试过程的概述](https://docs.microsoft.com/windows-hardware/drivers)。 此过程有助于确保构建一个可正常工作的驱动程序。

- 步骤9：为驱动程序创建驱动程序包。

  有关如何安装驱动程序的详细信息，请参阅[提供驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。 有关如何安装 NDIS 驱动程序的详细信息，请参阅[安装和升级网络组件](installing-and-upgrading-network-components.md)。

- 步骤10：对驱动程序进行签名和分发。

  最后一步是对驱动程序进行签名（可选）和分发。 如果你的驱动程序满足为[Windows 硬件兼容性计划](https://docs.microsoft.com/windows-hardware/design/compatibility/)定义的质量标准，你可以通过 Microsoft Windows 更新程序进行分发。 有关如何分发驱动程序的详细信息，请参阅[分发驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。

 

 





