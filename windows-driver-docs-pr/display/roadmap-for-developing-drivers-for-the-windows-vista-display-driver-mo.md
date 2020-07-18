---
title: Windows 显示驱动程序模型（WDDM）的道路图
description: 用于开发 Windows 显示驱动程序模型（WDDM）驱动程序的道路图
ms.assetid: 4f7ea2f4-ca2f-4b1d-97be-fb22e81c8080
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c6ebef19ed83695b36c4d1dddf184daea88028e9
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459247"
---
# <a name="road-map-for-the-windows-display-driver-model-wddm"></a>Windows 显示驱动程序模型（WDDM）的道路图

![用于开发 wddm 显示驱动程序的 wdk 路线图](images/wdkroadmap-th.png)

Windows 显示器驱动程序模型（WDDM）要求图形硬件供应商提供配对的用户模式显示驱动程序和内核模式显示驱动程序（或*显示微型端口驱动程序*）。

若要创建这些显示器驱动程序，请执行以下步骤：

- 步骤1：了解 Windows 体系结构和驱动程序。

  您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 请参阅[所有驱动程序开发人员的概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)。

- 步骤2：了解 WDDM 显示驱动程序的基础知识。

  若要了解基础知识，请参阅[Windows 显示驱动程序模型（WDDM）的简介](introduction-to-the-windows-vista-and-later-display-driver-model.md)、[视频内存管理和 GPU 计划](video-memory-management-and-gpu-scheduling.md)，以及[显示微型端口驱动程序的线程和同步模型](threading-and-synchronization-model-of-display-miniport-driver.md)。

    有关最近的 Windows 版本中的主要新功能的说明，请参阅[Windows 10 显示器和图形驱动程序的新增](https://docs.microsoft.com/windows-hardware/drivers/display/what-s-new-for-windows-10-display-and-graphics-drivers)功能

- 步骤3：了解用户模式显示驱动程序的信息，以及有关显示微型端口驱动程序的问题，请参阅[用户模式显示驱动](user-mode-display-drivers.md)程序和[多监视器和视频显示网络](multiple-monitors-and-video-present-networks.md)部分。

- 步骤4：了解 Windows 驱动程序的生成、测试和调试过程和工具。

  构建驱动程序与构建用户模式应用程序不同。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和驱动程序验证的信息，请参阅[开发、测试和部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/)。 有关生成、测试、验证和调试工具的信息，请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)。

- 步骤5：做出其他显示驱动程序设计决策。

  有关做出设计决策的信息，请参阅 windows 显示器驱动程序模型（ [wddm）中](tasks-in-the-windows-vista-display-driver-model.md) [Windows 显示驱动程序模型（Wddm）和任务的实现提示和要求](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)。

- 步骤6：访问并查看[显示驱动程序示例](display-samples.md)。

- 步骤7：开发、构建、测试和调试显示驱动程序。

  有关如何为图形适配器开发显示驱动程序的信息，请参阅[初始化显示微型端口和用户模式显示驱动](initializing-display-miniport-and-user-mode-display-drivers.md)程序和[Windows 显示驱动程序模型（WDDM）操作流](windows-vista-and-later-display-driver-model-operation-flow.md)。 有关迭代生成、测试和调试的信息，请参阅[开发、测试和部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 有关特定于显示驱动程序的调试提示，请参阅[WDDM 驱动程序的调试提示](debugging-tips-for-wddm-drivers.md)。 此过程有助于确保构建一个可正常工作的驱动程序。

- 步骤8：为显示驱动程序创建驱动程序包。

  有关详细信息，请参阅[分发驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/develop/distributing-a-driver-package-win8)。 有关如何安装图形适配器的显示驱动程序的信息，请参阅[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)。

- 步骤9：签署和分发您的显示驱动程序。

  最后一步是对驱动程序进行签名（可选）和分发。 如果你的驱动程序满足在[Windows 硬件实验室包](https://docs.microsoft.com/windows-hardware/test/hlk/)（以前称为 Windows 徽标包或 WLK）中定义的质量标准，你可以通过 Microsoft Windows 更新程序进行分发。 有关详细信息，请参阅[分发驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/develop/distributing-a-driver-package-win8)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。
