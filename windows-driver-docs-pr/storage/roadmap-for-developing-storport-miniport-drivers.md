---
title: Storport 微型端口驱动程序开发路线图
description: Storport 微型端口驱动程序开发路线图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c3a9315dd95210ace44015af0c00a8206c9323f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802193"
---
# <a name="roadmap-for-developing-storport-miniport-drivers"></a>Storport 微型端口驱动程序开发路线图

![图，该图中的文本 "wdk" 叠加在高速公路上](images/wdkroadmap-th.png)若要创建 storport 微型端口驱动程序，请执行以下步骤：

1. **了解 Windows 体系结构和驱动程序。**

    了解驱动程序在 Windows 中的工作原理的基础知识很重要。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

2. **了解 storport 微型端口驱动程序的基础知识。**

    若要了解 storport 微型端口驱动程序基础知识，请参阅 [Windows 存储驱动程序体系结构](storage-driver-architecture.md)、 [storport 提供的功能](capabilities-provided-by-storport.md)和 Storport [微型端口驱动程序的 storport 接口](storport-s-interface-with-storport-miniport-drivers.md)。

3. **确定附加的 storport 微型端口驱动程序设计决策。**

   有关如何制定设计决策的信息，请参阅 [Storport 提供的功能](capabilities-provided-by-storport.md)、 [存储类驱动程序的 storport 接口](storport-s-srb-interface-with-the-storage-class-driver.md)、 [存储虚拟小型端口驱动程序：何时适用](storage-virtual-miniport-drivers--when-are-they-appropriate-.md)，以及 [如何使 SCSI 端口微型驱动程序可与 Storport 一起使用](making-scsi-port-miniport-drivers-work-with-storport.md)。

4. **了解 Windows Vista 和更高版本的操作系统中的 storport 微型端口驱动程序。**

    请参阅 Windows 驱动程序工具包中 [的 Storport 历史记录](history-of-storport.md) (WDK) 。

5. **了解 Windows 驱动程序的生成、测试和调试过程和工具。**

   构建驱动程序与构建用户模式应用程序不同。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 Windows 徽标测试的信息，请参阅 [开发、测试和部署驱动程序](/windows-hardware/drivers) 。 有关生成、测试、验证和调试工具的信息，请参阅 [驱动程序开发工具](../devtest/index.md) 。

6. **查看 storport 微型端口驱动程序示例。**

    若要访问和查看 storport 微型端口驱动程序示例，请参阅 [Windows 驱动程序工具包 (WDK) 示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)。

7. **开发、构建、测试和调试 storport 微型端口驱动程序。**

    有关迭代生成、测试和调试的信息，请参阅 [构建驱动](../develop/building-a-driver.md)程序、 [测试驱动](/windows-hardware/drivers)程序和 [调试驱动程序](/windows-hardware/drivers) 。 此过程有助于确保构建一个可正常工作的驱动程序。

8. **为 storport 微型端口驱动程序创建驱动程序包。**

    有关详细信息，请参阅 [创建驱动程序包](/windows-hardware/drivers)。

9. **签署并分发你的 storport 微型端口驱动程序。**

    最后一步是 (可以选择) 签名和分发驱动程序。 如果你的驱动程序满足为 Windows 硬件认证定义的质量标准，你可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关详细信息，请参阅 [分发驱动程序包](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。
