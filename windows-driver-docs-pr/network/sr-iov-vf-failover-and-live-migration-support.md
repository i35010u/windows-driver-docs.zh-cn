---
title: SR-IOV VF 故障转移和实时迁移支持
description: SR-IOV VF 故障转移和实时迁移支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05a0b9a6563e3cb78ad6f49b8bb020dc3b9e2a71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803661"
---
# <a name="sr-iov-vf-failover-and-live-migration-support"></a>SR-IOV VF 故障转移和实时迁移支持


Hyper-v 子分区开始后，网络流量将流经合成数据路径。 如果物理网络适配器支持 (SR-IOV) 接口的单个根 i/o 虚拟化，则它可以启用一个或多个 PCI Express (PCIe) 虚拟函数 (VFs) 。 每个 VF 都可以附加到 Hyper-v 子分区。 发生这种情况时，网络流量将流经硬件优化 [SR-IOV VF 数据路径](sr-iov-vf-data-path.md)。

建立 VF 数据路径后，如果满足以下任一条件，则网络流量可以恢复为 [合成数据路径](sr-iov-vf-data-path.md) ：

-   VF 已附加到 Hyper-v 子分区，但会被分离。 例如，虚拟化堆栈可以将 VF 与一个子分区分离，并将其附加到另一个子分区。 如果正在运行的 Hyper-v 子分区比基础 SR-IOV 网络适配器上的 VF 资源多，则可能会发生这种情况。

    从 VF 数据路径故障转移到综合数据路径的过程称为 " *vf 故障转移*"。

-   Hyper-v 子分区正在实时迁移到另一台主机。

下图显示了通过 SR-IOV 网络适配器支持的各种数据路径。

![在管理父分区下显示 sr-iov 适配器的堆栈关系图，此管理父分区下的通信与 \# 包含使用 vm 总线通信的来宾操作系统的子分区1，而子分区 \# 2 则使用 vf 微型端口与 sr-iov 适配器进行通信](images/sriovdatapaths.png)

Netvsc.sys 公开 (VM) 网络适配器的虚拟机，该虚拟机绑定到 VF 微型端口驱动程序以支持 VF 数据路径。 在转换为合成数据路径的过程中，如果可能，从来宾操作系统中删除 VF 网络适配器。 如果无法正常删除 VF 并超时，则会将其意外删除。 然后，将停止 VF 微型端口驱动程序，并且网络虚拟服务客户端 (Netvsc.sys) 从 VF 微型端口驱动程序中解除绑定。

VF 与综合数据路径之间的转换会导致数据包的最小丢失，并防止丢失 TCP 连接。 在到综合数据路径的转换完成之前，虚拟化堆栈执行以下步骤：

1.  虚拟化堆栈将 VM 网络适配器的媒体访问控制 (MAC) 和虚拟 LAN (VLAN) 筛选器移动到连接到 PCIe 物理函数 (PF) 的默认虚拟端口 (VPort) 。 VM 网络适配器在子分区的来宾操作系统中公开。

    将筛选器移动到默认的 VPort 后，合成数据路径对于进出来宾操作系统中运行的网络组件的网络流量完全正常运行。 PF 微型端口驱动程序指示默认 PF VPort 上收到的数据包，该数据包使用综合数据路径指示到来宾操作系统的数据包。 同样，从来宾操作系统传输的所有数据包都将通过综合数据路径进行路由，并通过默认 PF VPort 传输。

    有关 VPorts 的详细信息，请参阅 [虚拟端口 (VPorts) ](virtual-ports--vports-.md)。

2.  虚拟化堆栈通过发出对象标识符 (OID 来删除附加到 VF 的 VPort) 将 [oid \_ NIC \_ SWITCH \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md) 请求发送到 PF 微型端口驱动程序。 微型端口驱动程序释放与 VPort 关联的任何硬件和软件资源并完成 OID 请求。

    有关详细信息，请参阅 [删除虚拟端口](deleting-a-virtual-port.md)。

3.  在释放虚拟化堆栈的资源之前，该虚拟化堆栈会请求 FLR 的一个 PCIe 函数级别重置 () 。 堆栈通过向 PF 微型端口驱动程序发出 [oid \_ SRIOV \_ RESET \_ VF](./oid-sriov-reset-vf.md)的 oid 集请求来实现此功能。 FLR 将 SR-IOV 网络适配器上的 VF 引入静态状态，并清除 VF 的任何挂起的中断事件。

4.  重置 VF 后，虚拟化堆栈会通过向 PF 微型端口驱动程序发出 [oid \_ NIC \_ 交换机 \_ 免费 \_ VF](./oid-nic-switch-free-vf.md) 的 OID 集请求来请求释放 VF 资源。 这会导致微型端口驱动程序释放与 VF 关联的硬件资源。

有关此过程的详细信息，请参阅 [虚拟函数拆卸序列](virtual-function-teardown-sequence.md)。

 

