---
title: 虚拟功能解除序列
description: 虚拟功能解除序列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 514b5e73ac866db544663efc0495762c5b90181b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802267"
---
# <a name="virtual-function-teardown-sequence"></a>虚拟功能解除序列


支持 (SR-IOV) 的单个根 i/o 虚拟化的网络适配器必须能够支持以下硬件组件：

-   一个 PCI Express (PCIe) 物理功能 (PF) 。 PF 始终存在于网络适配器上，并附加到 Hyper-v 父分区。

    有关此硬件组件的详细信息，请参阅 [Sr-iov 物理 Function (PF) ](sr-iov-physical-function--pf-.md)。

-   一个或多个 PCIe 虚拟功能 (VF) 。 必须将每个 VF 初始化并附加到 Hyper-v 子分区，来宾操作系统的网络组件才能通过 VF 发送或接收数据包。

    有关此硬件组件的详细信息，请参阅 [sr-iov)  (Sr-iov 虚拟函数 ](sr-iov-virtual-functions--vfs-.md)。

在 VF 分解并释放其资源之前，虚拟化堆栈会将虚拟 PCI (VPCI) 虚拟服务提供商通知 (VSP) 。 此 VSP 在 Hyper-v 父分区的管理操作系统中运行。 通知会通知 VPCI VSP VF 将从子分区断开并分离。 VPCI VSP 通过虚拟机总线将消息发送 (VMBus) 到子分区来宾操作系统中运行的 VPCI virtual service client (VSC) 。 这些消息请求 VPCI VSC 正常删除在将 VF 附加到子分区时公开的 VF 网络适配器。 这会导致 Netvsc.sys 从 VF 微型端口驱动程序和驱动程序中解除绑定。 此时，子分区中的数据包流量将从 VF 数据路径迁移到基于软件的合成数据路径。 有关这些数据路径的详细信息，请参阅 [Sr-iov 数据路径](sr-iov-data-paths.md)。

完成到综合数据路径的故障转移后，VF 会断开并释放其资源。 下图显示了与 VF 拆卸相关的步骤。

![示例 vf 拆卸序列，显示从虚拟化堆栈到 ndis 再到 pf 微型端口驱动程序的调用](images/sriov-vf-teardown.png)

在 VF 拆卸序列过程中，NDIS、虚拟化堆栈和 PF 微型端口驱动程序按照以下步骤进行操作：

1.  虚拟化堆栈将虚拟机 (VM) 网络适配器的媒体访问控制 (MAC) 和虚拟 LAN (VLAN) 筛选器移动到附加到 PF 的默认虚拟端口 (VPort) 。 VM 网络适配器在子分区的来宾操作系统中公开。

    Aftet 将筛选器移动到默认 VPort，合成数据路径对于进出来宾操作系统中运行的网络组件的网络流量完全可操作。 PF 微型端口驱动程序指示默认 PF VPort 上收到的数据包，该数据包使用综合数据路径指示到来宾操作系统的数据包。 同样，从来宾操作系统传输的所有数据包都将通过综合数据路径进行路由，并通过默认 PF VPort 传输。

2.  虚拟化堆栈通过发出对象标识符 (OID 来删除附加到 VF 的 VPort) 将 [oid \_ NIC \_ SWITCH \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md) 请求发送到 PF 微型端口驱动程序。 微型端口驱动程序释放与 VPort 关联的任何硬件或软件资源并完成 OID 请求。

    有关详细信息，请参阅 [删除虚拟端口](deleting-a-virtual-port.md)。

3.  在释放虚拟化堆栈的资源之前，该虚拟化堆栈会请求 FLR 的一个 PCIe 函数级别重置 () 。 堆栈通过向 PF 微型端口驱动程序发出 [oid \_ SRIOV \_ RESET \_ VF](./oid-sriov-reset-vf.md)的 oid 集请求来实现此功能。 FLR 将 SR-IOV 网络适配器上的 VF 引入静态状态，并清除 VF 的任何挂起的中断事件。

4.  重置 VF 后，虚拟化堆栈会通过向 PF 微型端口驱动程序发出 [oid \_ NIC \_ 交换机 \_ 免费 \_ VF](./oid-nic-switch-free-vf.md) 的 OID 集请求来请求释放 VF 资源。 这会导致微型端口驱动程序释放与 VF 关联的硬件资源。

 

