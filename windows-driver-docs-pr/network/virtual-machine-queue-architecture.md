---
title: 虚拟机队列体系结构
description: 虚拟机队列体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 412b0c30474eda7194ebc0476f57217876c61512
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802233"
---
# <a name="virtual-machine-queue-architecture"></a>虚拟机队列体系结构





NDIS 虚拟机队列 (VMQ) 体系结构提供了虚拟化的优势，例如：

-   虚拟化会影响性能，而 VMQ 有助于克服这些影响。

-   VMQ 支持实时迁移。

-   具有 NDIS 任务卸载和其他优化的 VMQ 共存。

本部分提供有关 NDIS VMQ 接口的高级信息。 在编写支持 VMQ 的 NDIS 驱动程序之前，应阅读此部分。 有关编写 VMQ 驱动程序的信息，请参阅 [编写 Vmq 驱动程序](writing-vmq-drivers.md)。

本节包括下列主题：

[NDIS 虚拟机队列 (VMQ) 简介](introduction-to-ndis-virtual-machine-queue--vmq-.md)

[NDIS 虚拟机 (VM) 共享内存的安全问题](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)

[NDIS VMQ 实时迁移支持](ndis-vmq-live-migration-support.md)

[NDIS VM 队列状态](ndis-virtual-machine-queue-states.md)

 

 





