---
title: Windows 显示驱动程序模型 (WDDM) 路线图
description: 开发 Windows 显示器驱动程序模型 (WDDM) 驱动程序的路线图
ms.assetid: 4f7ea2f4-ca2f-4b1d-97be-fb22e81c8080
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: aad2b93de22631e7c3f3a2ce0de4f31e743a7549
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365618"
---
# <a name="roadmap-for-the-windows-display-driver-model-wddm"></a>Windows 显示驱动程序模型 (WDDM) 路线图


![用于开发 wddm 的 wdk 路线图显示驱动程序](images/wdkroadmap-th.png)

Windows 显示驱动程序模型 (WDDM) 都需要图形硬件供应商提供的配对的用户模式显示驱动程序和内核模式显示驱动程序 (或*显示微型端口驱动程序*)。

若要创建这些文件显示驱动程序，请执行以下步骤：

-   第 1 步：了解 Windows 体系结构和驱动程序。

    你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并可用于简化开发过程。 请参阅[的所有驱动程序开发人员概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)。

-   步骤 2：了解基础知识的 WDDM 显示驱动程序。

    若要了解基础知识，请参阅[引入到 Windows 显示器驱动程序模型 (WDDM))](introduction-to-the-windows-vista-and-later-display-driver-model.md)，[视频内存管理和 GPU 计划](video-memory-management-and-gpu-scheduling.md)，和[线程处理和同步模型显示微型端口驱动程序](threading-and-synchronization-model-of-display-miniport-driver.md)。

    有关最新的 Windows 版本中的主要新功能的说明，请参阅：

    -   [What's new for Windows 8.1 显示器驱动程序 (WDDM 1.3)](what-s-new-for-windows-8-1-display-drivers--wddm-1-3-.md)
    -   [什么是 Windows 8 显示器驱动程序 (WDDM 1.2) 的新增功能](what-s-new-for-windows-8-display-drivers.md)
    -   [Windows 显示驱动程序模型增强 (WDDM 1.2)](https://go.microsoft.com/fwlink/p/?LinkId=226814)
-   步骤 3:了解有关用户模式显示驱动程序的信息和问题显示微型端口驱动程序从[用户模式显示驱动程序](user-mode-display-drivers.md)并[多个监视器和视频存在网络](multiple-monitors-and-video-present-networks.md)部分。

-   步骤 4：了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

    构建一个驱动程序不是与构建在用户模式应用程序相同。 请参阅[开发、 测试和部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers)有关 Windows 驱动程序生成、 调试和测试过程，驱动程序签名，以及驱动程序验证信息。 请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)有关生成、 测试、 验证和调试工具的信息。

-   步骤 5：使辅助显示器驱动程序的设计决策。

    制定设计决策有关的信息，请参阅[的实现技巧和要求的 Windows 显示器驱动程序模型 (WDDM)](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)并[任务中 Windows 显示器驱动程序模型 (WDDM)](tasks-in-the-windows-vista-display-driver-model.md)。

-   步骤 6：访问和查看在 WDK 中的显示驱动程序示例[显示示例](display-samples.md)。

-   步骤 7：开发、 生成、 测试和调试显示器驱动程序。

    有关如何开发您的图形适配器的显示器驱动程序的信息，请参阅[正在初始化显示微型端口和用户模式显示驱动程序](initializing-display-miniport-and-user-mode-display-drivers.md)和[Windows 显示驱动程序模型 (WDDM) 操作流](windows-vista-and-later-display-driver-model-operation-flow.md). 请参阅[开发、 测试和部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers)有关迭代构建、 测试和调试信息。 有关调试特定可以显示驱动程序的提示，请参阅[调试的提示的 Windows 显示驱动程序模型 (WDDM)](debugging-tips-for-the-windows-vista-display-driver-model.md)。 此过程将有助于确保您构建适用的驱动程序。

-   步骤 8：创建驱动程序包的显示器驱动程序。

    有关详细信息，请参阅[分发驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。 有关如何安装图形适配器的显示器驱动程序的信息，请参阅[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)。

-   步骤 9：签名和分发显示器驱动程序。

    最后一步是登录 （可选） 和分发该驱动程序。 如果您的驱动程序符合质量标准，中定义[Windows 硬件认证工具包](https://go.microsoft.com/fwlink/p/?linkid=248337)（以前称为 Windows Logo Kit 或 WLK），你可以将其分配通过 Microsoft Windows 更新计划。 有关详细信息，请参阅[分发驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 





