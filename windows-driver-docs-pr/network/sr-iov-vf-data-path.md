---
title: SR-IOV VF 数据路径
description: SR-IOV VF 数据路径
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 581d81ad5569f1a0e9855588e5154ce4970fd63f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840267"
---
# <a name="sr-iov-vf-data-path"></a>SR-IOV VF 数据路径


如果物理网络适配器支持 (SR-IOV) 接口的单个根 i/o 虚拟化，则它可以启用一个或多个 PCI Express (PCIe) 虚拟函数 (VFs) 。 每个 VF 都可以附加到 Hyper-v 子分区。 发生这种情况时，虚拟化堆栈会执行以下步骤：

1.  分配用于 VF 的资源后，虚拟化堆栈会为来宾操作系统中的 VF 公开一个网络适配器。 这会导致在来宾操作系统中运行的 PCI 驱动程序启动 VF 微型端口驱动程序。 此驱动程序由独立硬件供应商为 SR-IOV 网络适配器 (IHV) 提供。

    **注意**  VF 的资源必须由 PCIe 物理功能 (PF) 的微型端口驱动程序分配，然后才能将 VF 附加到 Hyper-v 子分区。 VF 资源包括将 NIC 交换机上 (VPort) 分配到 VF 的虚拟端口。 有关详细信息，请参阅 [Sr-iov 虚拟函数](sr-iov-virtual-functions--vfs-.md)。

2.  加载并初始化 VF 微型端口驱动程序后，NDIS 会将来宾操作系统中 (Netvsc.sys) 的网络虚拟服务客户端的协议边缘绑定到该驱动程序。

    **注意**  Netvsc.sys 仅绑定到 VF 微型端口驱动程序。 来宾操作系统中没有其他协议堆栈可以绑定到 VF 微型端口驱动程序。

Netvsc.sys 成功绑定到驱动程序后，来宾操作系统中的网络流量将通过 *VF 数据路径* 进行。 数据包是通过网络适配器的底层 VF 来发送或接收的，而不是基于软件的综合数据路径。 有关综合数据路径的详细信息，请参阅 [Sr-iov 合成数据路径](sr-iov-synthetic-data-path.md)。

下图显示了通过 SR-IOV 网络适配器的 VF 数据路径的组件。

![在管理父分区下显示 sr-iov 适配器的堆栈关系图，此管理父分区下的 pgf 微型端口和包含来宾操作系统的子分区使用 vf 小型端口进行通信](images/sriovvf-datapaths.png)

使用 VF 数据路径具有以下优势：

-   所有数据数据包直接在来宾操作系统中的网络组件和 VF 之间流动。 这消除了合成数据路径的开销，其中的数据包在 Hyper-v 子分区和父分区之间流动。

    有关综合数据路径的详细信息，请参阅 [Sr-iov 合成数据路径](sr-iov-synthetic-data-path.md)。

-   VF 数据路径会绕过来自 Hyper-v 子分区的数据包流量中的管理操作系统的任何干预。 VF 为它所附加到的子分区提供独立的内存空间、中断和 DMA 流。 这可实现与 nonvirtualized 环境几乎兼容的网络性能。

-   通过 VF 数据路径的数据包路由由 SR-IOV 网络适配器上的 NIC 交换机执行。 数据包通过适配器的物理端口通过外部网络发送或接收。 数据包也将与 VF 附加到的其他子分区相互转发。

    **注意**  与不附加 VF 的子分区之间的数据包将由 NIC 交换机转发到 Hyper-v 可扩展交换机模块。 此模块在 Hyper-v 父分区中运行，并使用综合数据路径将这些数据包传送到子分区。
