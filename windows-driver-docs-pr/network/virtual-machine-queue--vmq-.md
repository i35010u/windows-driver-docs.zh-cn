---
title: 虚拟机队列 (VMQ)
description: 虚拟机队列 (VMQ)
ms.assetid: c502c7d6-bdf1-4656-b5a5-339250910f08
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 285e8d2e07bf8519ab13fff81a5759a6f9698108
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353637"
---
# <a name="virtual-machine-queue-vmq"></a>虚拟机队列 (VMQ)





本部分介绍 NDIS 虚拟机队列 (VMQ) 接口。 VMQ 接口在 NDIS 6.20 和更高版本中 Windows Server 2008 R2 和更高版本的 Windows Server 支持 Microsoft HYPER-V 网络性能改进。

[虚拟机队列体系结构](virtual-machine-queue-architecture.md)文档介绍了 VMQ 体系结构的高级概念。 [编写 VMQ 驱动程序](writing-vmq-drivers.md)文档提供了有关编写驱动程序的 NDIS VMQ 的更多详细的信息。

**请注意**  务必研究[NDIS 虚拟微型端口驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617918)，尤其是 vmq.c 和 vmq.h 源文件。

 

支持 VMQ 接口：

-   通过使用目标媒体访问控制 (MAC) 地址将数据包路由到不同的网络适配器硬件中的接收数据包的分类接收队列。

-   NIC 可以使用 DMA 将数据包传送到虚拟机的直接共享内存。 有关共享内存的详细信息，请参阅[NDIS 内存管理界面](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

-   缩放到多个处理器，通过处理不同的处理器上的不同虚拟机的数据包。

本部分包括以下主题：

-   [虚拟机队列体系结构](virtual-machine-queue-architecture.md)
-   [编写 VMQ 驱动程序](writing-vmq-drivers.md)

 

 





