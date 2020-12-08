---
title: SR-IOV 合成数据路径
description: SR-IOV 合成数据路径
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d21add29092da81f7daaa73d5186005358ad048
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788277"
---
# <a name="sr-iov-synthetic-data-path"></a>SR-IOV 合成数据路径


当 Hyper-v 子分区启动并且来宾操作系统正在运行时，虚拟化堆栈会将 (Netvsc.sys) 启动网络虚拟服务客户端。 Netvsc.sys 公开 (VM) 网络适配器的虚拟机，该虚拟机向在来宾操作系统中运行的协议堆栈提供微型端口驱动程序边缘。

Netvsc.sys 还与 hyper-v 父分区的管理操作系统中运行的 Hyper-v 可扩展交换机通信。 可扩展交换机组件作为网络虚拟服务提供商 (NetVSP) 运行。 Netvsc.sys 和 NetVSP 之间的接口提供了一个称为 *合成数据路径* 的软件数据路径。

下图显示了通过 SR-IOV 网络适配器的综合数据路径的组件。

![在管理父分区下显示 sr-iov 适配器的堆栈关系图，该节点位于通过 vmbus 与包含来宾操作系统的子分区通信](images/sriovsynthetic-datapaths.png)

如果基础 SR-IOV 网络适配器分配 PCI Express (PCIe 的资源)  (VFs) 的虚拟功能，则虚拟化堆栈会将 VF 附加到 Hyper-v 子分区。 附加后，子分区内的数据包流量将通过硬件优化的 VF 数据路径而不是合成的数据路径进行。 有关 VF 数据路径的详细信息，请参阅 [Sr-iov 数据路径](sr-iov-data-paths.md)。

如果满足以下条件之一，则虚拟化堆栈可能仍会为 Hyper-v 子分区启用合成数据路径：

-   SR-IOV 网络适配器没有足够的 VF 资源来容纳所有已启动的 Hyper-v 子分区。 将网络适配器上的所有 VFs 附加到子分区后，其余分区将使用综合数据路径。

    从 VF 数据路径故障转移到综合数据路径的过程称为 " *vf 故障转移*"。

-   VF 已附加到 Hyper-v 子分区，但会被分离。 例如，虚拟化堆栈可以将 VF 与一个子分区分离，并将其附加到另一个子分区。 如果正在运行的 Hyper-v 子分区比基础 SR-IOV 网络适配器上的 VF 资源多，则可能会发生这种情况。

-   Hyper-v 子分区正在实时迁移到另一台主机。

尽管通过 SR-IOV 网络适配器的综合数据路径不如 VF 数据路径更高效，但仍可以对其进行硬件优化。 例如，如果配置了一个或多个 (VPorts) 的虚拟端口并将其附加到 PCIe 物理功能 (PF) ，则数据路径可以提供类似于虚拟机队列的卸载功能 (VMQ) 接口。 有关详细信息，请参阅 [非默认虚拟端口和 VMQ](nondefault-virtual-ports-and-vmq.md)。

 

 





