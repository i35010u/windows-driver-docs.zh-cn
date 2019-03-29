---
title: SR-IOV 数据路径概述
description: SR-IOV 数据路径概述
ms.assetid: C82AEB00-E699-40AB-85E8-064B841B83F4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb10aeafe3855b9c9288c2158f921e622d0d348b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577191"
---
# <a name="overview-of-sr-iov-data-paths"></a>SR-IOV 数据路径概述


当启动 HYPER-V 子分区，并且运行来宾操作系统时，虚拟化堆栈启动网络虚拟服务客户端 (NetVSC)。 NetVSC 通过提供到来宾操作系统中运行的协议堆栈的一个微型端口驱动程序边缘公开虚拟机 (VM) 网络适配器。 此外，NetVSC 还提供了一个协议驱动程序边缘，从而可以将绑定到基础微型端口驱动程序。

NetVSC 也与在 HYPER-V 父分区的管理操作系统中运行的 HYPER-V 可扩展交换机进行通信。 可扩展交换机组件用作网络虚拟服务提供商 (NetVSP)。 NetVSC 和 NetVSP 之间的接口提供的软件数据路径可以称为*综合数据路径*。 有关此数据路径的详细信息，请参阅[SR-IOV 综合数据路径](sr-iov-synthetic-data-path.md)。

如果物理网络适配器支持单根 I/O 虚拟化 (SR-IOV) 接口，它可以启用一个或多个 PCI Express (PCIe) 虚函数 (VFs)。 每个 VF 可以附加到 HYPER-V 子分区。 在此情况下，虚拟化堆栈将执行以下步骤：

1.  虚拟化堆栈的来宾操作系统中 VF 公开的网络适配器。 这将导致在启动 VF 微型端口驱动程序的来宾操作系统中运行的 PCI 驱动程序。 此驱动程序由独立硬件供应商 (IHV) 提供的 SR-IOV 网络适配器。

2.  加载和初始化 VF 微型端口驱动程序后，NDIS 将 NetVSC 协议边缘来宾操作系统中绑定到该驱动程序。

    **请注意**NetVSC 只绑定到 VF 微型端口驱动程序。 来宾操作系统中的任何其他协议堆栈可以不绑定到 VF 微型端口驱动程序。

通过 NetVSC 已成功将绑定到该驱动程序后，进行来宾操作系统中的网络流量*VF 数据路径*。 发送或通过基础 VF 而不是综合数据路径的网络适配器的接收数据包。

有关 VF 数据路径的详细信息，请参阅[SR-IOV VF 数据路径](sr-iov-vf-data-path.md)。

下图显示了支持 SR-IOV 网络适配器上的各种数据路径。

![显示与管理父分区的 sr-iov 适配器，并包含来宾操作系统的两个子分区的堆栈关系图](images/sriovdatapaths.png)

启动 HYPER-V 子分区并 VF 数据前建立路径后，网络流量将通过综合数据路径。 VF 数据路径建立后，网络流量可以还原到的综合数据路径，是否满足以下条件：

-   VF 变为未连接到 HYPER-V 子分区。 例如，虚拟化堆栈无法分离 VF 从一个子分区并将其附加到另一个子分区。 这可能不是基础的 SR-IOV 网络适配器上有 VF 资源运行的更多的 HYPER-V 子分区时。

    故障转移到的综合数据路径 VF 数据路径中的过程被称为*VF 故障转移*。

-   HYPER-V 子分区的实时迁移到另一台主机。

有关 VF 故障转移和实时迁移的详细信息，请参阅[SR-IOV VF 故障转移和实时迁移](sr-iov-vf-failover-and-live-migration-support.md)。