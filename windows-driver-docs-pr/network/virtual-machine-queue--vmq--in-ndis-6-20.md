---
title: NDIS 6.20 中的虚拟机队列 (VMQ)
description: NDIS 6.20 中的虚拟机队列 (VMQ)
keywords:
- 'NDIS 6.20 WDK，虚拟机队列 (VMQ) '
- 虚拟机队列 (VMQ) WDK NDIS 6.20
- VMQ WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7c7f0a89a964f9141ba70366db199a3f6708afa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802245"
---
# <a name="virtual-machine-queue-vmq-in-ndis-620"></a>NDIS 6.20 中的虚拟机队列 (VMQ)





NDIS 6.20 引入了虚拟机队列 (VMQ) 接口以支持 Microsoft Hyper-V 网络性能改进。 在初始化期间，NDIS 6.20 和更高版本的驱动程序必须提供有关 VMQ 功能的信息。 但是，VMQ 支持是可选的。

NDIS 6.20 和更高版本中的 VMQ 接口支持：

-   通过使用目标 MAC 地址将数据包路由到不同的接收队列来分类接收的数据包。

-   NIC 能够使用 DMA 将数据包直接传输到 Hyper-v 子分区的共享内存。

-   通过在不同处理器上处理不同 Hyper-v 分区的数据包来扩展到多个处理器。

Microsoft Hyper-V 的网络性能增强功能还为 Hyper-v 子分区提供无驱动程序更改的烟囱支持。

有关 VMQ 的详细信息，请参阅 [ (vmq) 虚拟机队列 ](virtual-machine-queue--vmq-.md)。

 

 





