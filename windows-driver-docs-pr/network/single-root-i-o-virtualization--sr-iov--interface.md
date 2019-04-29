---
title: 单根 I/O 虚拟化 (SR-IOV) 接口
description: 单根 I/O 虚拟化 (SR-IOV) 接口
ms.assetid: B65160F9-DB7E-427E-999C-09BD00173076
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a9827c11ea6cf76ccf7aac05b7fbf2c633e594d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363259"
---
# <a name="single-root-io-virtualization-sr-iov-interface"></a>单根 I/O 虚拟化 (SR-IOV) 接口


SR-IOV 接口允的 PCI Express (PCIe) 网络适配器上的硬件资源分区到一个或多个虚拟接口，称为*虚函数 (VFs)*。 这允许适配器资源在虚拟环境中共享。 SR-IOV 允许网络流量，以便通过将 VF 直接分配给 HYPER-V 子分区绕过虚拟软件切换层。 通过执行此操作，就会降低系统开销在软件仿真层中的 I/O 和网络吞吐量来实现与非虚拟化环境几乎相同的性能。

每个 PCIe VF 分配唯一的请求者 ID，允许 I/O 内存管理单元 (IOMMU) 来执行以下操作：

-   区分不同的流量流上的网络适配器的每个 PCIe 函数。 这允许 IOMMU 应用内存和中断翻译，以便这些通信流可以被直接发送到相应的子或父分区。

-   各个分区之间的隔离流量。 这可确保从分区的流量不会影响设备上的其他分区。

下图显示在 SR-IOV 接口 VF 数据路径。

![说明与 sr-iov 的合成设备数据路径的关系图](images/sriovarchitecture.png)

使用 VF 数据路径提供以下优势：

-   来宾操作系统中的协议堆栈和 VF 之间直接流动的数据的所有数据包。 这消除了哪些数据包之间的数据流的 HYPER-V 子和父分区中的综合数据路径的开销。 后转发到父分区，HYPER-V 可扩展交换机模块将转发到其他子分区或基础的 SR-IOV 物理适配器上的物理网络接口这些数据包。

-   VF 数据路径将由管理操作系统中的 HYPER-V 子分区中的数据包流量绕过用户参与。 VF 提供独立的存储空间、 中断和 DMA 流附加到的子分区。 这实现了与非虚拟化环境几乎兼容的网络性能。

-   通过 VF 数据路径路由数据包通过 NIC 来执行切换 SR-IOV 网络适配器上。 发送或通过外部网络适配器的物理端口通过接收数据包。 到或从取景器附加到其他子分区，同样会转发数据包。

    **请注意**  到或从分区没有取景器附加到转发的 NIC 的子包切换到可扩展交换机模块。 此模块在 HYPER-V 父分区中运行，并将这些数据包传递到子分区中，使用综合数据路径。

     

有关 SR-IOV 接口的详细信息，请参阅[单根 I/O 虚拟化 (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)。

 

 





