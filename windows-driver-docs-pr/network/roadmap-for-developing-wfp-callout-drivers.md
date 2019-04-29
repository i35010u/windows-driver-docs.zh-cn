---
title: WFP 标注驱动程序开发路线图
description: WFP 标注驱动程序开发路线图
ms.assetid: 98c857d9-e4a6-4a7f-8427-642763864f3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2adc5ad8cb592c802c571552553375e559a9b4d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359119"
---
# <a name="roadmap-for-developing-wfp-callout-drivers"></a>WFP 标注驱动程序开发路线图


若要创建 Windows 筛选平台 (WFP) 标注驱动程序，请执行以下步骤：

-   第 1 步：了解有关 WFP 体系结构。

    有关 WFP 的信息，请参阅[Windows 筛选平台](https://msdn.microsoft.com/library/windows/desktop/aa366510)。 您可能会发现，可以开发 WFP 用户模式应用程序并避免编写 WFP 标注驱动程序。

-   步骤 2：了解 Windows 体系结构和驱动程序。

    你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助你做出适当的设计决策，还可以简化开发过程。 有关驱动程序的基本原理的详细信息，请参阅[的所有驱动程序开发人员概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)。

-   步骤 3:确定您的 WFP 标注驱动程序的 Windows 驱动程序模型。

    WFP 标注驱动程序可以通过使用 Windows 驱动程序模型 (WDM) 或内核模式驱动程序框架 (KMDF) 编写。 有关如何选择驱动程序模型的详细信息，请参阅[选择驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff554652)。 WDM 有关详细信息，请参阅[Windows 驱动程序简介](https://msdn.microsoft.com/library/windows/hardware/ff548173)并[编写 WDM 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566412)。 有关 KMDF 详细信息，请参阅[WDF 驱动程序开发指南](https://msdn.microsoft.com/library/windows/hardware/dn265580)。

-   步骤 4：确定其他 Windows 驱动程序的设计决策。

    有关如何使更多 Windows 设计决策，请参阅[创建可靠的内核模式驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff542904)，[的 64 位驱动程序的编程问题](https://msdn.microsoft.com/library/windows/hardware/ff559923)，和[创建国际 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff540208)。

-   步骤 5：了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

    构建一个驱动程序不同于生成在用户模式应用程序。 有关 Windows 驱动程序生成、 调试和测试过程，驱动程序签名，并[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)测试，请参阅[构建、 调试和测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。 了解有关生成，测试、 验证和调试工具，请参阅[驱动程序开发工具](https://msdn.microsoft.com/library/windows/hardware/ff545440)。

-   步骤 6：审阅[Windows 筛选平台 (WFP) 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618680)中[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

-   步骤 7：做出有关 WFP 标注驱动程序的设计决策。

    有关如何设计 WFP 标注驱动程序的信息，请参阅[标注驱动程序编程注意事项](callout-driver-programming-considerations.md)。

-   步骤 8：开发、 生成、 测试和调试 WFP 标注驱动程序。

    有关 WFP 标注驱动程序详细信息，请参阅[标注驱动程序操作](callout-driver-operations.md)并[标注驱动程序安装](callout-driver-installation.md)。 有关函数、 结构、 枚举或特定于 WFP 的常量的信息，请参阅[Windows 筛选平台标注驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff571067)。 有关迭代构建、 测试和调试的信息，请参阅[概述的构建、 调试和测试过程](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。 此过程将有助于确保您构建适用的驱动程序。

-   步骤 9：创建 WFP 标注驱动程序的驱动程序包。

    有关详细信息，请参阅[提供一个驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)并[标注驱动程序安装](callout-driver-installation.md)。

-   步骤 10：签名和分发 WFP 标注驱动程序。

    最后一步是登录 （可选） 和分发该驱动程序。 如果您的驱动程序符合质量标准，为定义[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)，可以将其分配通过 Microsoft Windows 更新计划。 有关如何将驱动程序分发的详细信息，请参阅[分发驱动程序](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 





