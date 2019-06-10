---
title: 开发 Windows 存储驱动程序的路线图
description: 开发 Windows 存储驱动程序的路线图
ms.assetid: 67627ff9-588c-492f-861f-c592f7f92b51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8037c37e3b4c74f68f5c6fd3070d4550f9e7ad3
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815104"
---
# <a name="roadmap-for-developing-windows-storage-drivers"></a>开发 Windows 存储驱动程序的路线图


![示意图，带有文本"wdk"上一条高速公路上叠加的路线图](images/wdkroadmap-th.png)若要创建存储驱动程序，请执行以下步骤：

1.  **了解 Windows 体系结构和驱动程序。**

    你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并可用于简化开发过程。 请参阅[的所有驱动程序开发人员概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)。

2.  **了解存储驱动程序的基础知识。**

    若要了解存储驱动程序基础知识，请参阅[Windows 存储驱动程序体系结构](storage-driver-architecture.md)。

3.  **确定其他存储驱动程序的设计决策。**

    有关如何制定设计决策的信息，请参阅[功能提供的 Storport](capabilities-provided-by-storport.md)，[存储虚拟微型端口驱动程序：何时是否合适？](storage-virtual-miniport-drivers--when-are-they-appropriate-.md)，并[制定 SCSI 端口微型端口驱动程序使用 Storport](making-scsi-port-miniport-drivers-work-with-storport.md)。

4.  **了解有关 Windows 操作系统中的存储。**

    请参阅[Storport 的历史记录](history-of-storport.md)Windows 驱动程序工具包 (WDK) 中。

5.  **了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。**

    构建一个驱动程序不是与构建在用户模式应用程序相同。 请参阅[开发、 测试和部署驱动程序](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)Windows 驱动程序生成、 调试和测试过程，驱动程序签名，和 Windows 徽标测试有关的信息。 请参阅[驱动程序开发工具](https://msdn.microsoft.com/library/windows/hardware/ff545440)有关生成、 测试、 验证和调试工具的信息。

6.  **查看存储驱动程序示例。**

    访问和查看 storport 微型端口驱动程序示例请参阅[Windows Driver Kit (WDK) 示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)。

7.  **开发、 生成、 测试和调试您的存储驱动程序。**

    请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)，[测试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)，并[调试驱动程序](https://msdn.microsoft.com/windows-drivers/develop/debugging_a_driver)有关迭代构建、 测试和调试信息。 此过程将有助于确保您构建适用的驱动程序。

8.  **创建存储驱动程序的驱动程序包。**

    有关详细信息，请参阅[创建驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)。

9.  **签名并分发你的存储** **驱动程序。**

    最后一步是登录 （可选） 和分发该驱动程序。 如果您的驱动程序满足 Windows 硬件认证为定义的质量标准，您可以通过 Microsoft Windows Update 计划分发。 有关详细信息，请参阅[分发驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 




