---
title: 在 NDIS 6.30 中的虚拟化网络增强功能
description: 本部分介绍在 NDIS 6.30 中的虚拟化网络增强功能
ms.assetid: AA1EC2E2-2903-453A-B214-947CA3C4C931
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 425088b16b5406128b743dda55649e76a8990e6a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575507"
---
# <a name="virtualized-networking-enhancements-in-ndis-630"></a>NDIS 6.30 中的虚拟化网络增强


NDIS 支持虚拟化的网络接口，允许将 HYPER-V 父和子分区，以便进行交互的基础物理网络接口。

NDIS 6.20 包含虚拟机队列 (VMQ) 接口，以支持 Microsoft HYPER-V 网络性能改进。 有关 VMQ 的详细信息，请参阅[虚拟机队列 (VMQ)](virtual-machine-queue--vmq-.md)。

NDIS 6.30 扩展了对以下技术与虚拟化网络接口的支持，如中所述[概述的虚拟化网络](overview-of-virtualized-networking.md):

### <a name="single-root-io-virtualization-sr-iov"></a>单根 I/O 虚拟化 (SR-IOV)

SR-IOV 接口允的 PCI Express (PCIe) 网络适配器上的硬件资源分区到一个或多个虚拟接口，称为*虚函数 (VFs)*。 这允许适配器资源在虚拟环境中共享。 SR-IOV 允许网络流量，以便通过将 VF 直接分配给 HYPER-V 子分区绕过虚拟软件切换层。 通过执行此操作，就会降低系统开销在软件仿真层中的 I/O 和网络吞吐量来实现与非虚拟化环境几乎相同的性能。

有关 SR-IOV 接口的详细信息，请参阅[单根 I/O 虚拟化 (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)。

### <a name="hyper-v-extensible-switch"></a>Hyper-V 可扩展交换机

HYPER-V 可扩展交换机是在 HYPER-V 父分区的管理操作系统中运行的虚拟化以太网交换机。 可扩展交换机的每个实例连接到以下类型的网络适配器的端口之间路由数据包：

-   外部和内部网络适配器在运行 HYPER-V 父分区中管理操作系统中公开的。

-   综合或仿真网络适配器的 HYPER-V 子分区中运行来宾操作系统中公开的。

从 NDIS 6.30 开始，HYPER-V 可扩展交换机支持的可扩展性接口。 此接口允许 NDIS 筛选器驱动程序的实例 (称为*扩展*) 绑定中的 HYPER-V 可扩展交换机驱动程序堆栈。 绑定并驱动程序堆栈中启用后，扩展将面临可扩展交换机数据路径中的所有数据包流量。 这允许扩展监视、 修改和将数据包转发到可扩展的交换机端口。 这也允许扩展以检查并注入中各种 HYPER-V 分区都使用的虚拟网络接口的数据包。

有关 HYPER-V 可扩展交换机接口的详细信息，请参阅[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。

 

 





