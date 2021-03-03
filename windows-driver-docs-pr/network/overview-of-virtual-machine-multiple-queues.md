---
title: " (VMMQ) 的虚拟机的多个队列概述"
description: " (VMMQ) 的虚拟机的多个队列概述"
ms.date: 02/28/2021
ms.localizationpriority: medium
ms.openlocfilehash: 352e859871f79e02e5232d92f9751692ac978998
ms.sourcegitcommit: cf1f4196374c5b743448cb8d688d2223f7197d8f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2021
ms.locfileid: "101751965"
---
# <a name="overview-of-virtual-machine-multiple-queues-vmmq"></a> (VMMQ) 的虚拟机的多个队列概述


虚拟机多个队列 (VMMQ) 是一项 NIC 卸载技术，它将 [本机 RSS (RSSv1) ](introduction-to-receive-side-scaling.md) 扩展到 [hyper-v](overview-of-hyper-v.md) 虚拟环境。

VMMQ 为虚拟化节点的父分区中的 [虚拟端口 (VPorts) ](virtual-ports--vports-.md) 提供可缩放的网络流量处理。 VPort 表示网络适配器的 NIC 交换机上的内部端口，该端口支持 [ (sr-iov) 的单个根 i/o 虚拟化 ](overview-of-single-root-i-o-virtualization--sr-iov-.md)。 有关 SR-IOV 接口及其组件的概述，请参阅 [Sr-iov 体系结构](sr-iov-architecture.md)。 以前，RSS 处理不适用于 VPorts。 VMMQ 将本机 RSS 功能扩展到与 NIC (PF) （包括默认 VPort）关联的 VPorts。

VMMQ 可以有效地在 NIC 硬件中分配网络流量。 可以将多个硬件队列从 NIC 分配到单个 PF VPort。 NIC 使用 RSS 哈希将网络流量分布到这些队列中，将数据包直接放入分配的处理器。 将流量分配卸载到 NIC 可提高 CPU 性能，因为软件无需完成此任务。

你可能想要启用 VMMQ 功能以减少主机 CPU 消耗，并通过将 CPU 负载分散到多个处理器上，为虚拟系统启用更高的吞吐量。 可以将 VMMQ 支持添加到新的或现有的 NDIS 6.60 及更高版本的驱动程序。 如果适配器支持 VMMQ，则驱动程序由供应商提供，操作系统为 Windows Server 2019，则默认情况下启用 VMMQ。 如果适配器不支持 VMMQ，则驱动程序由系统提供，或者操作系统为 Windows Server 2016，则默认情况下，VMMQ 处于禁用状态或不可用。 如果操作系统早于 Windows Server 2016，则 VMMQ 不可用。

VMMQ 可用于父分区中公开的 VPorts，而不管 NIC 是在 [sr-iov](overview-of-single-root-i-o-virtualization--sr-iov-.md) 中运行还是 [ (VMQ) 模式虚拟机队列 ](virtual-machine-queue--vmq-.md) 。



## <a name="expected-feature-interactions"></a>预期功能交互

- [使用通用路由封装的网络虚拟化 (NVGRE) ](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md) 和 [虚拟广泛的局域网 (VXLAN) ](/windows-server/networking/sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server#VXLAN)： NIC 将根据数据包的内部标头来计算用于传播接收队列的哈希。

- [Sr-iov](overview-of-single-root-i-o-virtualization--sr-iov-.md)： NIC 可以同时支持 VMMQ 和 sr-iov。

## <a name="in-this-section"></a>在本节中

[VMMQ 发送和接收处理](vmmq-send-and-receive-processing.md)

[广告 VMMQ 功能](advertising-vmmq-capabilities.md)

[VMMQ 的标准化 INF 关键字](standardized-inf-keywords-for-vmmq.md)

[为 VMMQ 分配 VPorts](allocating-vports-for-vmmq.md)

[启用、禁用和更新 VPort 上的 VMMQ](updating-vmmq-on-a-vport.md)
