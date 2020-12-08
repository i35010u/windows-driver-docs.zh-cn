---
title: NDIS 6.30 中的虚拟化网络增强功能
description: 本部分介绍 NDIS 6.30 中虚拟化的网络增强功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77f7c36ddfc4de6d42cacb840c591a944370183b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836687"
---
# <a name="virtualized-networking-enhancements-in-ndis-630"></a>NDIS 6.30 中的虚拟化网络增强


NDIS 支持虚拟化网络接口，该接口允许 Hyper-v 父分区和子分区建立基础物理网络接口的接口。

NDIS 6.20 包含虚拟机队列 (VMQ) 接口以支持 Microsoft Hyper-V 网络性能改进。 有关 VMQ 的详细信息，请参阅 [ (vmq) 虚拟机队列 ](virtual-machine-queue--vmq-.md)。

如 [虚拟化网络概述](overview-of-hyper-v.md)中所述，NDIS 6.30 将对虚拟化网络接口的支持扩展为以下技术：

### <a name="single-root-io-virtualization-sr-iov"></a>单根 I/O 虚拟化 (SR-IOV)

SR-IOV 接口允许将 PCI Express (PCIe) 网络适配器上的硬件资源分区为一个或多个虚拟接口，这些接口称为 *虚拟功能 (VFs)*。 这允许在虚拟环境中共享适配器资源。 SR-IOV 使网络流量能够通过将 VF 直接分配给 Hyper-v 子分区，绕过虚拟软件交换机层。 这样，软件仿真层中的 i/o 开销就会降低，并且网络吞吐量实现的性能与在非虚拟化环境中的性能几乎相同。

有关 SR-IOV 接口的详细信息，请参阅 [单一根 I/o 虚拟化 (sr-iov) ](single-root-i-o-virtualization--sr-iov-.md)。

### <a name="hyper-v-extensible-switch"></a>Hyper-V 可扩展交换机

Hyper-v 可扩展交换机是在 Hyper-v 父分区的管理操作系统中运行的虚拟化以太网交换机。 可扩展交换机的每个实例在连接到以下类型的网络适配器的端口之间路由数据包：

-   在管理操作系统中公开的、在 Hyper-v 父分区中运行的外部和内部网络适配器。

-   在 Hyper-v 子分区中运行的来宾操作系统中公开的合成或仿真网络适配器。

从 NDIS 6.30 开始，Hyper-v 可扩展交换机支持扩展接口。 此接口允许将 NDIS 筛选器驱动程序的实例 (称为 *扩展*) 在 Hyper-v 可扩展交换机驱动程序堆栈中进行绑定。 在驱动程序堆栈内绑定和启用后，扩展将公开到可扩展交换机数据路径中的所有数据包流量。 这样，扩展可以监视、修改数据包并将数据包转发到可扩展的交换机端口。 这样，扩展还可以在虚拟网络接口中检查和注入各种 Hyper-v 分区使用的数据包。

有关 Hyper-v 可扩展交换机接口的详细信息，请参阅 [Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)。

 

 





