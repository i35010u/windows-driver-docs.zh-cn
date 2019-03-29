---
title: SR-IOV VF 数据路径
description: SR-IOV VF 数据路径
ms.assetid: 0DC2327E-3A58-46BC-A3D6-3AFD24ABC901
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55582ede1f934862e1aca9890dc5c3d7561f166e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567521"
---
# <a name="sr-iov-vf-data-path"></a>SR-IOV VF 数据路径


如果物理网络适配器支持单根 I/O 虚拟化 (SR-IOV) 接口，它可以启用一个或多个 PCI Express (PCIe) 虚函数 (VFs)。 每个 VF 可以附加到 HYPER-V 子分区。 在此情况下，虚拟化堆栈将执行以下步骤：

1.  一旦 VF 的资源的分配，虚拟化堆栈的来宾操作系统中 VF 公开的网络适配器。 这将导致在启动 VF 微型端口驱动程序的来宾操作系统中运行的 PCI 驱动程序。 此驱动程序由独立硬件供应商 (IHV) 提供的 SR-IOV 网络适配器。

    **请注意**VF 资源必须在由微型端口驱动程序 PCIe 物理函数 (PF) 为之前分配 VF 可以附加到 HYPER-V 子分区。 VF 资源包括到 VF NIC 交换机上分配的虚拟端口 (VPort)。 有关详细信息，请参阅[SR-IOV 虚拟功能](sr-iov-virtual-functions--vfs-.md)。

2.  加载和初始化 VF 微型端口驱动程序后，NDIS 将网络虚拟服务客户端 (NetVSC) 的协议边缘来宾操作系统中绑定到该驱动程序。

    **请注意**NetVSC 只绑定到 VF 微型端口驱动程序。 来宾操作系统中的任何其他协议堆栈可以不绑定到 VF 微型端口驱动程序。

通过 NetVSC 已成功将绑定到该驱动程序后，进行来宾操作系统中的网络流量*VF 数据路径*。 发送或通过基础 VF 而不是基于软件的综合数据路径的网络适配器的接收数据包。 综合数据路径的详细信息，请参阅[SR-IOV 综合数据路径](sr-iov-synthetic-data-path.md)。

下图显示了 SR-IOV 网络适配器上的 VF 数据路径的组件。

![堆栈图示下方管理父分区进行通信使用 pgf 微型端口和子分区包含来宾操作系统进行通信使用 vf sr-iov 适配器微型端口](images/sriovvf-datapaths.png)

使用 VF 数据路径提供以下优势：

-   来宾操作系统中的网络组件和 VF 之间直接流动的数据的所有数据包。 这消除了哪些数据包之间的数据流的 HYPER-V 子和父分区中的综合数据路径的开销。

    综合数据路径的详细信息，请参阅[SR-IOV 综合数据路径](sr-iov-synthetic-data-path.md)。

-   VF 数据路径将由管理操作系统中的 HYPER-V 子分区中的数据包流量绕过用户参与。 VF 提供独立的存储空间、 中断和 DMA 流附加到的子分区。 这实现了与非虚拟化环境几乎兼容的网络性能。

-   通过 VF 数据路径路由数据包通过 NIC 来执行切换 SR-IOV 网络适配器上。 发送或通过外部网络适配器的物理端口通过接收数据包。 到或从取景器附加到其他子分区，同样会转发数据包。

    **请注意**到或从分区没有取景器附加到转发的 NIC 的子包切换到 HYPER-V 可扩展交换机模块。 此模块在 HYPER-V 父分区中运行，并将这些数据包传递到子分区中，使用综合数据路径。