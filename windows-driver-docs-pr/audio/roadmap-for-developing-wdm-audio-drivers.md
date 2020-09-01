---
title: 开发 WDM 音频驱动程序的路线图
description: 开发 WDM 音频驱动程序的路线图
ms.assetid: fa75ff65-32fe-4002-89fd-bf345502a9ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a77992a79ebe2bc053431a7940f1995ca8dc665
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210413"
---
# <a name="roadmap-for-developing-wdm-audio-drivers"></a>开发 WDM 音频驱动程序的路线图


![图，该图中的文本 "wdk" 叠加在高速公路上](images/wdkroadmap-th.png)音频驱动程序基于 Windows 驱动程序模型 (WDM) 。

若要创建 WDM 音频驱动程序，请执行以下步骤：

1.  **了解 Windows 体系结构和驱动程序。**

    您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

2.  **了解 WDM 音频驱动程序的基础知识。**

    Windows 操作系统版本从 Windows XP 到 Windows Vista 的音频驱动程序符合 WDM，并使用内核流组件。 若要了解必须做出的驱动程序设计决策，请参阅 [内核流式处理](../stream/kernel-streaming.md)、 [Wdm 音频驱动程序概述](getting-started-with-wdm-audio-drivers.md) 和 [wdm 音频驱动程序简介](introduction-to-wdm-audio-drivers.md)。

3.  **确定其他 WDM 音频驱动程序设计决策。**

    有关如何做出设计决策的信息，请参阅 [自定义音频驱动程序](custom-audio-drivers.md)、 [音频数据格式和数据范围](audio-data-formats-and-data-ranges.md)。 如果需要帮助确定要了解的音频驱动程序类型，请参阅 [自定义音频驱动程序类型决策树](custom-audio-driver-type-decision-tree.md)。

4.  **了解音频处理对象。**

    音频处理对象 () ，为 Windows 音频流提供可自定义的基于软件的数字信号处理。 若要了解详细信息，请参阅 [Windows 音频处理对象](windows-audio-processing-objects.md)。

5.  **了解 Windows 驱动程序的生成、测试和调试过程和工具。**

    构建驱动程序与构建用户模式应用程序不同。 有关 Windows 驱动程序生成、调试和测试过程的信息，请参阅 [开发、测试和部署驱动](/windows-hardware/drivers) 程序和驱动程序签名。 有关生成、测试、验证和调试工具的信息，请参阅 [驱动程序开发工具](../devtest/index.md) 。

6.  **查看 WDK 中的音频驱动程序示例。**

    若要访问和查看 WDK 中的音频驱动程序示例，请参阅 [示例音频驱动程序](sample-audio-drivers.md)。

7.  **做出关于 WDM 音频驱动程序的设计决策。**

    请参阅[内核中的](com-in-the-kernel.md)[音频微型端口驱动程序](audio-miniport-drivers.md)和 COM。

8.  **开发、构建、测试和调试 WDM 音频驱动程序。**

    有关如何为特定音频适配器开发音频驱动程序的信息，请参阅 [适配器驱动程序构造](adapter-driver-construction.md)。 有关迭代生成、测试和调试的信息，请参阅 [开发、测试和部署驱动程序](/windows-hardware/drivers) 。 此过程有助于确保构建一个可正常工作的驱动程序。

9.  **为 WDM 音频驱动程序创建驱动程序包。**

    有关详细信息，请参阅 [创建驱动程序包](/windows-hardware/drivers)。 有关如何安装音频适配器的信息，请参阅 [安装端口类音频适配器](installing-a-port-class-audio-adapter.md)。

10. **签署和分发 WDM 音频驱动程序。**

    最后一步是对 (可选) 进行签名，然后分发驱动程序。 如果你的驱动程序满足为 Windows 认证计划定义的质量标准，你可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关详细信息，请参阅 [分发驱动程序包](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。

 

