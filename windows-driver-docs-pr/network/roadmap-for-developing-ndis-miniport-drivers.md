---
title: 开发 NDIS 微型端口驱动程序的路线图
description: 开发 NDIS 微型端口驱动程序的路线图
ms.assetid: 7cb56c08-3578-49d7-a0aa-a89dc6b139ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 104b2bc044be9958ca1937ccb5f3a1b02bcfecfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545237"
---
# <a name="roadmap-for-developing-ndis-miniport-drivers"></a>开发 NDIS 微型端口驱动程序的路线图


若要创建的网络驱动程序接口规范 (NDIS) 微端口驱动程序包，请执行以下步骤：

- 第 1 步：了解 Windows 体系结构和驱动程序。

  你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助你做出适当的设计决策，还可以简化开发过程。 有关驱动程序的基本原理的详细信息，请参阅[的所有驱动程序开发人员概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)。

- 步骤 2：了解有关 NDIS。

  有关常规信息有关 NDIS 和 NDIS 驱动程序，请参阅以下主题：

  [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

  [网络驱动程序的编程注意事项](network-driver-programming-considerations.md)

  [驱动程序堆栈管理](driver-stack-management.md)

  [NET\_缓冲体系结构](net-buffer-architecture.md)

- 步骤 3:确定其他 Windows 驱动程序的设计决策。

  详细了解如何使更多 Windows 设计决策，请参阅[创建可靠的内核模式驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff542904)，[的 64 位驱动程序的编程问题](https://msdn.microsoft.com/library/windows/hardware/ff559923)，和[创建国际 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff540208)。

- 步骤 4：了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

  构建一个驱动程序不同于生成在用户模式应用程序。 Windows 驱动程序生成、 调试和测试过程，驱动程序签名，有关详细信息和[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)测试，请参阅[构建、 调试和测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。 有关生成的详细信息，测试、 验证和调试工具，请参阅[驱动程序开发工具](https://msdn.microsoft.com/library/windows/hardware/ff545440)。

- 步骤 5：阅读微型端口驱动程序简介主题。
  [类型的 NDIS 微型端口驱动程序](types-of-ndis-miniport-drivers.md)
  [网络接口卡支持](network-interface-card-support.md)
  [微型端口驱动程序代码的重要功能](important-features-of-miniport-driver-code.md)
   [示例 NDIS 微型端口驱动程序](sample-ndis-miniport-drivers.md)
- 步骤 6：读取[编写微型端口驱动程序部分](writing-ndis-miniport-drivers.md)。

  本部分中概述的主微型端口驱动程序接口。 这些接口包括微型端口驱动程序提供的函数 (*MiniportXxx*函数) 和 NDIS 调用启动的操作。 提供了 NDIS **Ndis * Xxx*** 函数会执行 NDIS 操作该微型端口驱动程序调用。

- 步骤 7：审阅[NDIS 微型端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918)中[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

- 步骤 8: （可选读取） 的其他注意事项微型端口驱动程序。

  其他注意事项包括展开中所述的主接口的主题[编写微型端口驱动程序部分](writing-ndis-miniport-drivers.md)。

  [获取和设置微型端口驱动程序信息和对 WMI 的 NDIS 支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)

  [NDIS MSI-X](ndis-msi-x.md)

  [NDIS 散播-聚集 DMA](ndis-scatter-gather-dma.md)

  [NDIS 电源管理](ndis-power-management.md)

  [Plug and Play NDIS 微型端口驱动程序](plug-and-play-for-ndis-miniport-drivers.md)

  [重置、 停止和关闭函数](reset--halt--and-shutdown-functions.md)

  [使用 WDM 低界面的微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff560532)

  [WAN 微型端口驱动程序](wan-miniport-drivers.md)

  [可伸缩网络](https://msdn.microsoft.com/library/windows/hardware/ff570735)

- 步骤 9：开发 （或端口），生成、 测试和调试您的 NDIS 驱动程序。

  如果要将迁移现有驱动程序移植指导，请参阅：

  -   [移植到 NDIS 6.0 的 NDIS 5.x 驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [移植到 NDIS 6.20 NDIS 6.x 驱动程序](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [移植到 NDIS 6.30 NDIS 6.x 驱动程序](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  有关迭代构建、 测试和调试的详细信息，请参阅[概述的构建、 调试和测试过程](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。 此过程将有助于确保您构建适用的驱动程序。

- 步骤 10：创建您的驱动程序的驱动程序包。

  有关如何安装驱动程序的详细信息，请参阅[提供一个驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)。 有关如何安装的 NDIS 驱动程序的详细信息，请参阅[安装和升级网络组件](installing-and-upgrading-network-components.md)。

- 步骤 11：签名和分发您的驱动程序。

  最后一步是登录 （可选） 和分发该驱动程序。 如果您的驱动程序符合质量标准，为定义[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)，可以将其分配通过 Microsoft Windows 更新计划。 有关如何将驱动程序分发的详细信息，请参阅[分发驱动程序](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 





