---
title: 单根 I/O 虚拟化 (SR-IOV) 接口
description: 单根 I/O 虚拟化 (SR-IOV) 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36350935c8eced1253c2f6b36ddc70584f502bb7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828441"
---
# <a name="single-root-io-virtualization-sr-iov-interface"></a>单根 I/O 虚拟化 (SR-IOV) 接口


SR-IOV 接口允许将 PCI Express (PCIe) 网络适配器上的硬件资源分区为一个或多个虚拟接口，这些接口称为 *虚拟功能 (VFs)*。 这允许在虚拟环境中共享适配器资源。 SR-IOV 使网络流量能够通过将 VF 直接分配给 Hyper-v 子分区，绕过虚拟软件交换机层。 这样，软件仿真层中的 i/o 开销就会降低，网络吞吐量达到与 nonvirtualized 环境中几乎相同的性能。

为每个 PCIe VF 分配一个唯一的请求者 ID，该 ID 允许 i/o 内存管理单元 (IOMMU) 执行以下操作：

-   区分网络适配器每个 PCIe 功能上不同的流量流。 这样，IOMMU 就可以应用内存和中断转换，以便可以将这些流量直接传递到适当的子分区或父分区。

-   隔离分区之间的流量流。 这可以保证来自分区的流量不会影响设备上的其他分区。

下图显示了 SR-IOV 接口内的 VF 数据路径。

![用 sr-iov 说明综合设备数据路径的示意图](images/sriovarchitecture.png)

使用 VF 数据路径具有以下优势：

-   所有数据数据包直接在来宾操作系统中的协议堆栈和 VF 之间流动。 这消除了合成数据路径的开销，其中的数据包在 Hyper-v 子分区和父分区之间流动。 一旦转发到父分区，Hyper-v 可扩展交换机模块就会将这些数据包转发到其他子分区或底层 SR-IOV 物理适配器上的物理网络接口。

-   VF 数据路径会绕过来自 Hyper-v 子分区的数据包流量中的管理操作系统的任何干预。 VF 为它所附加到的子分区提供独立的内存空间、中断和 DMA 流。 这可实现与 nonvirtualized 环境几乎兼容的网络性能。

-   通过 VF 数据路径的数据包路由由 SR-IOV 网络适配器上的 NIC 交换机执行。 数据包通过适配器的物理端口通过外部网络发送或接收。 数据包也将与 VF 附加到的其他子分区相互转发。

    **注意**  发件人与未附加 VF 的子分区之间的数据包将由 NIC 交换机转发到可扩展交换机模块。 此模块在 Hyper-v 父分区中运行，并使用综合数据路径将这些数据包传送到子分区。

     

有关 SR-IOV 接口的详细信息，请参阅 [单一根 I/o 虚拟化 (sr-iov) ](single-root-i-o-virtualization--sr-iov-.md)。

 

 





