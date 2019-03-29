---
title: SR-IOV VF 故障转移和实时迁移支持
description: SR-IOV VF 故障转移和实时迁移支持
ms.assetid: 93D6EFC7-B701-4D10-8114-FA437E80096B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 764a4c1297dda8282014042edcc75abcb9a3b011
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575885"
---
# <a name="sr-iov-vf-failover-and-live-migration-support"></a>SR-IOV VF 故障转移和实时迁移支持


启动 HYPER-V 子分区后，网络流量将通过综合数据路径。 如果物理网络适配器支持单根 I/O 虚拟化 (SR-IOV) 接口，它可以启用一个或多个 PCI Express (PCIe) 虚函数 (VFs)。 每个 VF 可以附加到 HYPER-V 子分区。 在此情况下，通过硬件优化网络流量的流动[SR-IOV VF 数据路径](sr-iov-vf-data-path.md)。

建立 VF 数据路径之后，可以还原到的网络流量[综合数据路径](sr-iov-vf-data-path.md)如果任意下列条件为 true:

-   VF 已附加到 HYPER-V 子分区，但将变为已分离。 例如，虚拟化堆栈无法分离 VF 从一个子分区并将其附加到另一个子分区。 这可能不是基础的 SR-IOV 网络适配器上有 VF 资源运行的更多的 HYPER-V 子分区时。

    故障转移到的综合数据路径 VF 数据路径中的过程被称为*VF 故障转移*。

-   HYPER-V 子分区的实时迁移到另一台主机。

下图显示了支持 SR-IOV 网络适配器上的各种数据路径。

![堆栈图示下方管理父分区进行通信使用子分区与通信的虚拟机总线 sr-iov 适配器\#通信使用的虚拟机来宾操作系统 1 包含总线，此外子分区\#2 通信时使用到的 sr-iov 适配器 vf 微型端口](images/sriovdatapaths.png)

NetVSC 公开绑定到 VF 微型端口驱动程序以支持 VF 数据路径的虚拟机 (VM) 网络适配器。 在转换为的综合数据路径，期间 VF 删除网络适配器是正常如有可能从来宾操作系统。 如果不能正常和时间出删除 VF，它将是意外删除。 然后暂停 VF 微型端口驱动程序，以及网络虚拟服务客户端 (NetVSC) 是从 VF 微型端口驱动程序未绑定。

VF 和综合数据路径之间的转换的数据包丢失最少会出现，并且可以防止 TCP 连接丢失。 为综合数据路径转换已完成之前，虚拟化堆栈将按照以下步骤：

1.  虚拟化堆栈将 VM 网络适配器的媒体访问控制 (MAC) 和虚拟 LAN (VLAN) 的筛选器移到附加到 PCIe 物理函数 (PF) 的默认虚拟端口 (VPort)。 VM 网络适配器的子分区在来宾操作系统中公开。

    筛选器移动到默认 VPort 后，综合数据路径是完全可操作的网络流量与来宾操作系统中运行的网络组件。 PF 微型端口驱动程序指示默认 PF VPort 综合数据路径用于指示将数据包用于来宾操作系统上的接收的数据包。 同样，从来宾操作系统的所有传输的数据包是通过综合数据路径路由，并且通过默认 PF VPort 传输。

    有关 VPorts 详细信息，请参阅[虚拟端口 (VPorts)](virtual-ports--vports-.md)。

2.  虚拟化堆栈中删除通过发出的对象标识符 (OID) 组请求附加到 VF VPort [OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)到 PF微型端口驱动程序。 微型端口驱动程序，释放与 VPort 关联任何硬件和软件资源并完成 OID 请求。

    有关详细信息，请参阅[删除虚拟端口](deleting-a-virtual-port.md)。

3.  虚拟化堆栈请求 PCIe 函数级别重置 (FLR) 的 VF 之前释放其资源。 通过发出的 OID 集请求的堆栈实现这[OID\_SRIOV\_重置\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451889)到 PF 微型端口驱动程序。 FLR VF SR-IOV 网络适配器上引入静止状态，并为 VF 清除任何挂起的中断事件。

4.  虚拟化堆栈 VF 已被重置后，通过发出 OID 集请求的请求的 VF 资源释放[OID\_NIC\_交换机\_免费\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)到 PF微型端口驱动程序。 这将导致微型端口驱动程序，以释放与 VF 相关联的硬件资源。

有关此过程的详细信息，请参阅[虚拟函数拆卸序列](virtual-function-teardown-sequence.md)。

 

 





