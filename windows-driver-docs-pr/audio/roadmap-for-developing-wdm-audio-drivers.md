---
title: 开发 WDM 音频驱动程序的路线图
description: 开发 WDM 音频驱动程序的路线图
ms.assetid: fa75ff65-32fe-4002-89fd-bf345502a9ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 418557c8a8fda820cbcb872787d3697c8d220761
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355278"
---
# <a name="roadmap-for-developing-wdm-audio-drivers"></a>开发 WDM 音频驱动程序的路线图


![示意图，带有文本"wdk"上一条高速公路上叠加的路线图](images/wdkroadmap-th.png)音频驱动程序基于 Windows 驱动程序模型 (WDM)。

若要创建 WDM 音频驱动程序，请执行以下步骤：

1.  **了解 Windows 体系结构和驱动程序。**

    你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并可用于简化开发过程。 请参阅[的所有驱动程序开发人员概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)。

2.  **了解 WDM 音频驱动程序的基础知识。**

    从 Windows XP 到 Windows Vista 的 Windows 操作系统版本中的音频驱动程序符合 WDM，并且使用内核流式处理组件。 若要了解必须进行的驱动程序设计决策，请参阅[流式处理内核](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)， [WDM 音频驱动程序概述](getting-started-with-wdm-audio-drivers.md)并[WDM 音频驱动程序简介](introduction-to-wdm-audio-drivers.md)。

3.  **确定其他 WDM 音频驱动程序的设计决策。**

    有关如何制定设计决策的信息，请参阅[自定义音频驱动程序](custom-audio-drivers.md)，[音频数据格式和数据范围](audio-data-formats-and-data-ranges.md)。 如果需要帮助来确定类型的音频驱动程序以了解有关的信息，请参阅[自定义音频驱动程序类型决策树](custom-audio-driver-type-decision-tree.md)。

4.  **了解有关音频处理对象。**

    音频处理对象 (Apo) 提供 Windows 音频流的可自定义软件基于数字信号处理。 若要了解详细信息，请参阅[Windows 音频处理对象](windows-audio-processing-objects.md)。

5.  **了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。**

    构建一个驱动程序不是与构建在用户模式应用程序相同。 请参阅[开发、 测试和部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers)有关 Windows 驱动程序生成、 调试和测试过程和驱动程序签名的信息。 请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)有关生成、 测试、 验证和调试工具的信息。

6.  **查看在 WDK 中的音频驱动程序示例。**

    若要访问和查看在 WDK 中的音频驱动程序示例，请参阅[示例音频驱动程序](sample-audio-drivers.md)。

7.  **做出有关 WDM 音频驱动程序的设计决策。**

    请参阅[音频微型端口驱动程序](audio-miniport-drivers.md)并[内核中的 COM](com-in-the-kernel.md)。

8.  **开发、 生成、 测试和调试 WDM 音频驱动程序。**

    有关如何开发您的特定音频适配器的音频驱动程序的信息，请参阅[适配器驱动程序构造](adapter-driver-construction.md)。 请参阅[开发、 测试和部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers)有关迭代构建、 测试和调试信息。 此过程将有助于确保您构建适用的驱动程序。

9.  **创建 WDM 音频驱动程序的驱动程序包。**

    有关详细信息，请参阅[创建驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。 有关如何安装的音频的适配器的信息，请参阅[安装端口类音频适配器](installing-a-port-class-audio-adapter.md)。

10. **签名和分发 WDM 音频驱动程序。**

    最后一步是登录 （可选） 和分发该驱动程序。 如果您的驱动程序符合质量标准，为 Windows 认证计划定义，您可以通过 Microsoft Windows Update 计划分发。 有关详细信息，请参阅[分发驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 




