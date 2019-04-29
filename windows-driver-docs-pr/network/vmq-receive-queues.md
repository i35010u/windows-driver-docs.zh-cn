---
title: VMQ 接收队列
description: VMQ 接收队列
ms.assetid: 9c34b437-97f7-49fa-afcd-16f1c238828a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82f5b13b1f8b5289e20161bbb9175a3bbbc66c4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327613"
---
# <a name="vmq-receive-queues"></a>VMQ 接收队列





虚拟机队列 (VMQ) 服务提供程序分配 VMQ 接收队列。 如果数据包通过队列设置的筛选器测试，网络适配器硬件会将传入的网络数据包分配给队列。

VMQ 接收队列具有以下属性：

-   一个队列标识符，是唯一的关联的网络适配器。

-   中断的处理器关联。

-   队列设置的筛选器。

-   接收到队列分配的缓冲区。

此外，还有默认队列具有以下属性：

-   默认队列始终存在。 必须分配其他队列。

-   默认的队列接收未通过其他队列的筛选器测试的数据包。

微型端口驱动程序为与 VMQ 相关联的接收缓冲区分配共享的内存。 具体取决于 Windows Server 版本中，微型端口驱动程序必须遵循以下各节所述的缓冲区分配的指导原则：

-   [VMQ 接收分配共享的内存缓冲区 (Windows Server 2008 R2)](#windows7)

-   [分配共享的内存 VMQ 接收缓冲区 （Windows Server 2012 和更高版本）](#windows8)

VMQ 共享内存要求设计为地址的虚拟机 (Vm) 的潜在安全问题。 VMQ 安全问题的详细信息，请参阅[NDIS 虚拟机 (VM) 共享内存的安全问题](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)。

### <a href="" id="windows7"></a>VMQ 接收分配共享的内存缓冲区 (Windows Server 2008 R2)

有关 Windows Server 2008 R2 中的 NDIS 6.20，如果微型端口驱动程序支持数据包数据拆分到单独的预测先行缓冲区，它可以分配共享的内存如下所示：

-   微型端口驱动程序为预预期缓冲区从管理操作系统运行的 HYPER-V 父分区中的地址空间分配的共享的内存。 Pre 预期缓冲区是由管理操作系统检查数据包的一部分。

-   微型端口驱动程序为运行 HYPER-V 子分区中的来宾操作系统的地址空间中的 post 预测先行缓冲区分配的共享的内存。 开机自检预期缓冲区是由来宾操作系统来检查数据包的一部分。

    **请注意**  HYPER-V 子分区也称为是 VM。

     

下图显示的共享的内存中队列、 管理操作系统和来宾操作系统。

![说明了队列管理操作系统分区，以及 vm 分区中的共享的内存关系图](images/vmqaddress.png)

在图中，从管理操作系统地址空间分配的标头信息和从来宾操作系统地址空间分配的数据显示在队列中的每个数据包。

### <a href="" id="windows8"></a>分配共享的内存 VMQ 接收缓冲区 （Windows Server 2012 和更高版本）

从开始 NDIS 6.30，拆分 VMQ 缓冲区接收到单独的预测先行缓冲区不再受支持。 微型端口驱动程序必须为每个从管理操作系统的地址空间的接收缓冲区分配内存。

 

 





