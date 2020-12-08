---
title: SR-IOV 数据路径概述
description: SR-IOV 数据路径概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f28ef402bc37a20e890457a547ccf779c0413d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815929"
---
# <a name="overview-of-sr-iov-data-paths"></a>SR-IOV 数据路径概述


当 Hyper-v 子分区启动并且来宾操作系统正在运行时，虚拟化堆栈会将 (Netvsc.sys) 启动网络虚拟服务客户端。 Netvsc.sys 通过向在来宾操作系统中运行的协议堆栈提供微型端口驱动程序边缘，来公开虚拟机 (VM) 网络适配器。 此外，Netvsc.sys 还提供了一个协议驱动程序边缘，使其可以绑定到基础微型端口驱动程序。

Netvsc.sys 还与 hyper-v 父分区的管理操作系统中运行的 Hyper-v 可扩展交换机通信。 可扩展交换机组件作为网络虚拟服务提供商 (NetVSP) 运行。 Netvsc.sys 和 NetVSP 之间的接口提供了一个称为 *合成数据路径* 的软件数据路径。 有关此数据路径的详细信息，请参阅 [Sr-iov 合成数据路径](sr-iov-synthetic-data-path.md)。

如果物理网络适配器支持 (SR-IOV) 接口的单个根 i/o 虚拟化，则它可以启用一个或多个 PCI Express (PCIe) 虚拟函数 (VFs) 。 每个 VF 都可以附加到 Hyper-v 子分区。 发生这种情况时，虚拟化堆栈会执行以下步骤：

1.  虚拟化堆栈为来宾操作系统中的 VF 公开了一个网络适配器。 这会导致在来宾操作系统中运行的 PCI 驱动程序启动 VF 微型端口驱动程序。 此驱动程序由独立硬件供应商为 SR-IOV 网络适配器 (IHV) 提供。

2.  加载并初始化 VF 微型端口驱动程序后，NDIS 会将来宾操作系统中 Netvsc.sys 的协议边缘绑定到该驱动程序。

    **注意**  Netvsc.sys 仅绑定到 VF 微型端口驱动程序。 来宾操作系统中没有其他协议堆栈可以绑定到 VF 微型端口驱动程序。

Netvsc.sys 成功绑定到驱动程序后，来宾操作系统中的网络流量将通过 *VF 数据路径* 进行。 数据包是通过网络适配器的底层 VF 而不是合成数据路径发送或接收的。

有关 VF 数据路径的详细信息，请参阅 [SR-IOV VF 数据路径](sr-iov-vf-data-path.md)。

下图显示了通过 SR-IOV 网络适配器支持的各种数据路径。

![显示具有管理父分区和包含来宾操作系统的两个子分区的 sr-iov 适配器的堆栈关系图](images/sriovdatapaths.png)

在启动 Hyper-v 子分区并建立 VF 数据路径之前，网络流量将流经合成数据路径。 建立 VF 数据路径后，如果满足以下条件，网络流量可以恢复为合成数据路径：

-   VF 将与 Hyper-v 子分区无关。 例如，虚拟化堆栈可以将 VF 与一个子分区分离，并将其附加到另一个子分区。 如果正在运行的 Hyper-v 子分区比基础 SR-IOV 网络适配器上的 VF 资源多，则可能会发生这种情况。

    从 VF 数据路径故障转移到综合数据路径的过程称为 " *vf 故障转移*"。

-   Hyper-v 子分区正在实时迁移到另一台主机。

有关 VF 故障转移和实时迁移的详细信息，请参阅 [SR-IOV VF 故障转移和实时迁移](sr-iov-vf-failover-and-live-migration-support.md)。
