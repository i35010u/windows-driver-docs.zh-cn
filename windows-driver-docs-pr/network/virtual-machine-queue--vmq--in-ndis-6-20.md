---
title: 在 NDIS 6.20 中的虚拟机队列 (VMQ)
description: 在 NDIS 6.20 中的虚拟机队列 (VMQ)
ms.assetid: fb48b019-4646-426d-b10e-d760788f9985
keywords:
- NDIS 6.20 WDK，虚拟机队列 (VMQ)
- 虚拟机队列 (VMQ) WDK NDIS 6.20
- VMQ WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df2443645c7ce6614b57d3eb2f25dd8880cb10b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545333"
---
# <a name="virtual-machine-queue-vmq-in-ndis-620"></a>在 NDIS 6.20 中的虚拟机队列 (VMQ)





NDIS 6.20 引入了虚拟机队列 (VMQ) 接口，以支持 Microsoft HYPER-V 网络性能改进。 NDIS 6.20 和更高版本的驱动程序必须提供有关 VMQ 功能在初始化过程中的信息。 但是，VMQ 的支持是可选的。

在 NDIS 6.20 和更高版本支持 VMQ 接口：

-   通过使用目标 MAC 地址来将数据包路由到不同的接收数据包的分类接收队列。

-   NIC 可以使用 DMA 将数据包传送到 HYPER-V 子分区的直接共享内存。

-   缩放到多个处理器，通过处理不同的处理器上的不同的 HYPER-V 分区的数据包。

Microsoft HYPER-V 网络性能增强功能还为烟囱支持 HYPER-V 子分区不进行任何驱动程序更改。

有关 VMQ 的详细信息，请参阅[虚拟机队列 (VMQ)](virtual-machine-queue--vmq-.md)。

 

 





