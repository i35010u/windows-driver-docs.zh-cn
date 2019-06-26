---
title: MB 微型端口驱动程序开发路线图
description: MB 微型端口驱动程序开发路线图
ms.assetid: 3ef6e899-22dc-4293-80cc-d786b03c6b29
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f444c121fa0680e2feaf3539b3acd1fd48750c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382164"
---
# <a name="roadmap-to-develop-mb-miniport-drivers"></a>MB 微型端口驱动程序开发路线图


若要创建 MB 微型端口驱动程序，请执行以下步骤：

-   **步骤 1**：了解 Windows 体系结构和微型端口驱动程序。

    你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助你做出适当的设计决策，还可以简化开发过程。 有关驱动程序的基本原理的详细信息，请参阅[的所有驱动程序开发人员概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)。

-   **步骤 2**:了解 MB 微型端口驱动程序的基础知识。

    MB 微型端口驱动程序支持 Windows 7 和更高版本的 Windows 中，并符合*NDIS 6.20 规范*。 若要了解必须做的微型端口驱动程序设计决策，请参阅[简介 NDIS 6.20](introduction-to-ndis-6-20.md)。

-   **步骤 3**:确定其他 Windows 驱动程序的设计决策。

    有关如何使更多 Windows 设计决策，请参阅[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)，[的 64 位驱动程序的编程问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)，和[创建国际 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

-   **步骤 4**:了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

    构建一个驱动程序不同于生成用户模式应用程序。 有关 Windows 驱动程序生成、 调试和测试过程，驱动程序签名，并[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)测试，请参阅[构建、 调试和测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 了解有关生成，测试、 验证和调试工具，请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)。

-   **步骤 5**:做出有关 MB 微型端口驱动程序的设计决策。

    有关详细信息，请参阅[MB 接口概述](mb-interface-overview.md)。 此外可以了解有关如何通过查看开发移动宽带的微型端口驱动程序的详细信息[移动宽带设备驱动程序开发](https://go.microsoft.com/fwlink/p/?linkid=144416)白皮书。

-   **步骤 6**:开发、 生成、 测试和调试 MB 微型端口驱动程序。

    有关迭代构建、 测试和调试的信息，请参阅[概述的构建、 调试和测试过程](https://docs.microsoft.com/windows-hardware/drivers)。 此过程将有助于确保生成的工作的微型端口驱动程序。

-   **步骤 7**:创建 MB 微型端口驱动程序的驱动程序包。

    有关详细信息，请参阅[提供一个驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。

-   **步骤 8**:签名和分发 MB 微型端口驱动程序。

    最后一步是登录 （可选） 和分发微型端口驱动程序。 微型端口驱动程序是否符合为定义的质量标准[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)，可以将其分配通过 Microsoft Windows 更新计划。 有关如何将驱动程序分发的详细信息，请参阅[分发驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

这些是基本步骤。 其他步骤可能需要根据各个微型端口驱动程序的需求。

 

 





