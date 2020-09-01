---
title: MB 微型端口驱动程序开发路线图
description: MB 微型端口驱动程序开发路线图
ms.assetid: 3ef6e899-22dc-4293-80cc-d786b03c6b29
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f45eee143abccecc62b021d1f790b33a330edfce
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211603"
---
# <a name="roadmap-to-develop-mb-miniport-drivers"></a>MB 微型端口驱动程序开发路线图


若要创建 MB 微型端口驱动程序，请执行以下步骤：

-   **步骤 1**：了解 Windows 体系结构和微型端口驱动程序。

    您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅 [所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

-   **步骤 2**：了解 MB 微型端口驱动程序的基础知识。

    Windows 7 和更高版本的 Windows 支持 MB 微型端口驱动程序，并且符合 *NDIS 6.20 规范*。 若要了解必须进行的微型端口驱动程序设计决策，请参阅 [NDIS 6.20 简介](introduction-to-ndis-6-20.md)。

-   **步骤 3**：确定其他 Windows 驱动程序设计决策。

    有关如何进行其他 Windows 设计决策的信息，请参阅 [创建可靠的内核模式驱动程序](../kernel/creating-reliable-kernel-mode-drivers.md)、 [64 位驱动程序的编程问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)以及 [创建国际 INF 文件](../install/creating-international-inf-files.md)。

-   **步骤 4**：了解 Windows 驱动程序的生成、测试和调试过程和工具。

    构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 测试的信息，请参阅 [生成、调试和测试驱动程序](/windows-hardware/drivers)。 有关生成、测试、验证和调试工具的信息，请参阅 [驱动程序开发工具](../devtest/index.md)。

-   **步骤 5**：做出关于 MB 微型端口驱动程序的设计决策。

    有关详细信息，请参阅 [MB 界面概述](mb-interface-overview.md)。 还可以通过查看 [移动宽带驱动程序开发](https://go.microsoft.com/fwlink/p/?linkid=144416) 白皮书来了解有关如何开发移动宽带微型端口驱动程序的详细信息。

-   **步骤 6**：开发、构建、测试和调试 MB 微型端口驱动程序。

    有关迭代生成、测试和调试的信息，请参阅 [生成、调试和测试过程的概述](/windows-hardware/drivers)。 此过程有助于确保构建一个可正常使用的微型端口驱动程序。

-   **步骤 7**：为 MB 微型端口驱动程序创建驱动程序包。

    有关详细信息，请参阅 [提供驱动程序包](/windows-hardware/drivers)。

-   **步骤 8**：签署和分发您的 MB 微型端口驱动程序。

    最后一步是对 (可选) 进行签名，并分发微型端口驱动程序。 如果您的微型端口驱动程序满足为 [Windows 硬件认证工具包 ](https://go.microsoft.com/fwlink/p/?LinkId=733613)定义的质量标准 (HCK) ，则可以通过 Microsoft Windows 更新计划分发该驱动程序。 有关如何分发驱动程序的详细信息，请参阅 [分发驱动程序](/windows-hardware/drivers)。

这些是基本步骤。 根据单个小型端口驱动程序的需要，可能需要执行其他步骤。

 

