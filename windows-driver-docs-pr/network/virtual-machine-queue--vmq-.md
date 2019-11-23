---
title: 虚拟机队列 (VMQ) 概述
description: 虚拟机队列 (VMQ) 概述
ms.assetid: c502c7d6-bdf1-4656-b5a5-339250910f08
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c49c74bfd2784c934f4984dbd626891e8794057a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842952"
---
# <a name="virtual-machine-queue-vmq-overview"></a>虚拟机队列 (VMQ) 概述

本部分介绍 NDIS 虚拟机队列（VMQ）接口。 VMQ 接口支持在 Windows Server 2008 R2 和更高版本的 Windows server 中的 NDIS 6.20 和更高版本中 Microsoft Hyper-V 的网络性能改进。

[虚拟机队列体系结构](virtual-machine-queue-architecture.md)文档介绍了 VMQ 体系结构的高级概念。 [编写 VMQ 驱动程序](writing-vmq-drivers.md)文档提供了有关编写 NDIS VMQ 驱动程序的更详细信息。

**请注意**  一定要研究[NDIS 虚拟微端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918)，尤其是 vmq 和 vmq 源文件。

 

VMQ 接口支持：

-   通过使用目标媒体访问控制（MAC）地址将数据包路由到不同的接收队列来分类网络适配器硬件中接收的数据包。

-   NIC 能够使用 DMA 将数据包直接传输到虚拟机的共享内存。 有关共享内存的详细信息，请参阅[NDIS 内存管理接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

-   通过处理不同处理器上不同虚拟机的数据包，缩放到多个处理器。

本部分包括以下主题：

-   [虚拟机队列体系结构](virtual-machine-queue-architecture.md)
-   [写入 VMQ 驱动程序](writing-vmq-drivers.md)