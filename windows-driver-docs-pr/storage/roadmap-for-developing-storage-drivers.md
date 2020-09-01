---
title: 开发 Windows 存储驱动程序的路线图
description: 开发 Windows 存储驱动程序的路线图
ms.assetid: 67627ff9-588c-492f-861f-c592f7f92b51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2c87d967840f9bdf1da34ae3b104c8926feffdb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188010"
---
# <a name="roadmap-for-developing-windows-storage-drivers"></a>开发 Windows 存储驱动程序的路线图


![图，该图中的文本 "wdk" 叠加在高速公路上](images/wdkroadmap-th.png)若要创建存储驱动程序，请执行以下步骤：

1.  **了解 Windows 体系结构和驱动程序。**

    您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

2.  **了解存储驱动程序的基础知识。**

    若要了解存储驱动程序基础知识，请参阅 [Windows 存储驱动程序体系结构](storage-driver-architecture.md)。

3.  **确定其他存储驱动程序设计决策。**

    有关如何做出设计决策的信息，请参阅 [Storport 提供的功能](capabilities-provided-by-storport.md)、 [存储虚拟微型端口驱动程序：何时适用](storage-virtual-miniport-drivers--when-are-they-appropriate-.md)，以及 [如何使 SCSI 端口微型驱动程序与 Storport 一起工作](making-scsi-port-miniport-drivers-work-with-storport.md)。

4.  **了解 Windows 操作系统中的存储。**

    请参阅 Windows 驱动程序工具包中 [的 Storport 历史记录](history-of-storport.md) (WDK) 。

5.  **了解 Windows 驱动程序的生成、测试和调试过程和工具。**

    构建驱动程序与构建用户模式应用程序不同。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 Windows 徽标测试的信息，请参阅 [开发、测试和部署驱动程序](/windows-hardware/drivers) 。 有关生成、测试、验证和调试工具的信息，请参阅 [驱动程序开发工具](../devtest/index.md) 。

6.  **查看存储驱动程序示例。**

    若要访问和查看 storport 微型端口驱动程序示例，请参阅 [Windows 驱动程序工具包 (WDK) 示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)。

7.  **开发、构建、测试和调试你的存储驱动程序。**

    有关迭代生成、测试和调试的信息，请参阅 [构建驱动](../develop/building-a-driver.md)程序、 [测试驱动](/windows-hardware/drivers)程序和 [调试驱动程序](/windows-hardware/drivers) 。 此过程有助于确保构建一个可正常工作的驱动程序。

8.  **为存储驱动程序创建驱动程序包。**

    有关详细信息，请参阅 [创建驱动程序包](/windows-hardware/drivers)。

9.  **签名并分发你的存储****驱动程序。**

    最后一步是对 (可选) 进行签名，然后分发驱动程序。 如果你的驱动程序满足为 Windows 硬件认证定义的质量标准，你可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关详细信息，请参阅 [分发驱动程序包](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。

 

