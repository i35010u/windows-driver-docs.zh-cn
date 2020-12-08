---
title: VMQ 接收队列
description: VMQ 接收队列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bada836844db054443d5a37e1828be121862bbb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786713"
---
# <a name="vmq-receive-queues"></a>VMQ 接收队列





虚拟机队列 (VMQ) 服务提供程序分配 VMQ 接收队列。 如果数据包通过了在队列中设置的筛选器测试，网络适配器硬件会将传入网络数据包分配给队列。

VMQ 接收队列具有以下属性：

-   一个队列标识符，它对于关联的网络适配器是唯一的。

-   中断的处理器关联。

-   在队列中设置的筛选器。

-   接收分配给队列的缓冲区。

还有一个默认队列，它具有以下属性：

-   默认队列始终存在。 必须分配其他队列。

-   默认队列接收未通过其他队列的筛选器测试的数据包。

微型端口驱动程序为与 VMQ 关联的接收缓冲区分配共享内存。 根据 Windows Server 版本，微型端口驱动程序必须遵循以下部分中所述的有关缓存分配的准则：

-   [为 VMQ 接收缓冲区分配共享内存 (Windows Server 2008 R2) ](#windows7)

-   [为 VMQ 接收缓冲区分配共享内存 (Windows Server 2012 及更高版本) ](#windows8)

VMQ 共享内存要求旨在解决 (Vm) 的虚拟机的潜在安全问题。 有关 VMQ 安全问题的详细信息，请参阅 [ (VM) 共享内存的 NDIS 虚拟机的安全问题](security-issues-with-ndis-virtual-machine--vm--shared-memory.md)。

### <a name="allocating-shared-memory-for-vmq-receive-buffers-windows-server-2008-r2"></a><a href="" id="windows7"></a>为 VMQ 接收缓冲区分配共享内存 (Windows Server 2008 R2) 

对于 Windows Server 2008 R2 中的 NDIS 6.20，如果微型端口驱动程序支持将数据包数据拆分为单独的预测先行缓冲区，则可以按以下方式分配共享内存：

-   小型端口驱动程序通过在 Hyper-v 父分区中运行的管理操作系统的地址空间为预先预测缓冲区分配共享内存。 预先预测缓冲区是由管理操作系统检查的数据包的一部分。

-   小型端口驱动程序通过在 Hyper-v 子分区中运行的来宾操作系统的地址空间为后续预测后缓冲区分配共享内存。 后先行预测缓冲区是来宾操作系统检查的数据包部分。

    **注意**  Hyper-v 子分区也称为 VM。

     

下图显示了队列、管理操作系统和来宾操作系统中的共享内存。

![说明队列中的共享内存、管理操作系统分区和 vm 分区的关系图](images/vmqaddress.png)

在此图中，队列中的每个数据包都显示在从管理操作系统地址空间中分配的标头信息和从来宾操作系统地址空间分配的数据。

### <a name="allocating-shared-memory-for-vmq-receive-buffers-windows-server-2012-and-later-versions"></a><a href="" id="windows8"></a>为 VMQ 接收缓冲区分配共享内存 (Windows Server 2012 及更高版本) 

从 NDIS 6.30 开始，不再支持将 VMQ 接收缓冲区拆分为单独的预测缓冲区。 微型端口驱动程序必须从管理操作系统的地址空间为每个接收缓冲区分配内存。

 

 





