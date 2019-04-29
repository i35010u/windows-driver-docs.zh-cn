---
title: 虚拟机队列体系结构
description: 虚拟机队列体系结构
ms.assetid: 7aa8c9a4-1bb2-48a5-be28-9806e16d4e94
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf2813ad11f895e1c5d8a7bdcbf08ab6bd7bbba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378227"
---
# <a name="virtual-machine-queue-architecture"></a>虚拟机队列体系结构





NDIS 虚拟机队列 (VMQ) 体系结构如提供虚拟化的优点：

-   虚拟化会影响性能和 VMQ 可帮助克服这些效果。

-   VMQ 支持实时迁移。

-   使用 NDIS 任务卸载和其他优化共存 VMQ。

本部分提供有关 NDIS VMQ 接口的高级信息。 在编写支持 VMQ 的 NDIS 驱动程序之前，应阅读此部分。 有关编写 VMQ 驱动程序的信息，请参阅[编写 VMQ 驱动程序](writing-vmq-drivers.md)。

本部分包括以下主题：

[NDIS 虚拟机队列 (VMQ) 简介](introduction-to-ndis-virtual-machine-queue--vmq-.md)

[使用 NDIS 虚拟机 (VM) 的安全问题共享内存](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)

[NDIS VMQ 实时迁移支持](ndis-vmq-live-migration-support.md)

[NDIS VM 队列状态](ndis-virtual-machine-queue-states.md)

 

 





