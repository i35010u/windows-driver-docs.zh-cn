---
title: 虚拟功能初始化序列
description: 虚拟功能初始化序列
ms.assetid: 352E12EC-FAF0-4566-8632-B6DA97ACCAD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11a86525cd4d55bba3f227d154dff8d3c02540f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345973"
---
# <a name="virtual-function-initialization-sequence"></a>虚拟功能初始化序列


支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器必须能够支持以下硬件组件：

-   一个 PCI Express (PCIe) 物理函数 (PF)。 PF 始终存在于网络适配器上并附加到 HYPER-V 父分区。

    有关此硬件组件的详细信息，请参阅[SR-IOV 物理函数 (PF)](sr-iov-physical-function--pf-.md)。

-   一个或多个 PCIe 虚拟函数 (VF)。 必须初始化每个取景器，并将其来宾操作系统的网络组件才能发送或接收数据包通过取景器附加到 HYPER-V 子分区。

    有关此硬件组件的详细信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

PF 微型端口驱动程序，可以在管理操作系统的 HYPER-V 父分区中运行，初始化并为 VF SR-IOV 网络适配器上分配资源。 NDIS 调用 PF 微型端口驱动程序的后[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数、 NDIS 和虚拟化堆栈可以对象标识符 (OID) 向发出请求 PF 微型端口驱动程序来执行以下操作：

-   网络适配器上创建一个 NIC 开关。 NIC 切换 VFs、 pf，PF 和物理网络端口之间的桥网络流量。

    有关详细信息，请参阅[NIC 开关](nic-switches.md)。

    **请注意**从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。



-   请求 PF 微型端口驱动程序，以初始化并为网络适配器上 VF 分配的资源。

    有关详细信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

-   NIC 交换机上创建虚拟端口 (VPort) 并将其附加到 VF。

    有关详细信息，请参阅[虚拟端口 (VPorts)](virtual-ports--vports-.md)。

下图显示了与 VF 初始化所涉及的步骤。

![显示来自虚拟化堆栈的调用到 ndis，再到 pf 微型端口驱动程序示例 vf 初始化序列](images/sriov-vf-initialization.png)

NDIS、 虚拟化堆栈和 PF 微型端口驱动程序 VF 初始化序列期间执行以下步骤：

1.  NDIS 从注册表读取默认交换机配置，并发出的 OID 方法请求[OID\_NIC\_切换\_创建\_切换](https://msdn.microsoft.com/library/windows/hardware/hh451815)来预配网络中的交换机适配器。 在此 OID 请求中传递的参数包括有关如何配置 VFs 和 VPorts 等重要硬件资源的信息。 它还包括有关如何分发附加到 PF.在非默认 VPorts 和默认 VPort 之间的资源

    OID 已成功完成 PF 微型端口驱动程序后，已准备好用于创建 VPorts 并对其分配 VFs NIC 开关。

    有关如何创建 NIC 交换机的详细信息，请参阅[创建 NIC 切换](creating-a-nic-switch.md)。

2.  VF 视为一种用于虚拟机 (VM) 网络适配器的卸载机制。 此适配器的 HYPER-V 子分区中运行来宾操作系统中公开。 默认情况下，来宾操作系统中的网络组件通过发送和接收数据包的基于软件的综合数据路径。 但是，如果启用子分区以进行 VF 卸载虚拟化堆栈 OID 对发出请求的资源分配和初始化 VF 的 PF 微型端口驱动程序。 取景器附加到子分区和 VPort NIC 交换机上的后，网络组件通过发送和接收数据包 VF 数据路径。 有关这些数据路径的详细信息，请参阅[SR-IOV 数据路径](sr-iov-data-paths.md)。

    如果为 VF 卸载、 虚拟化堆栈问题 OID 方法请求的已启用 HYPER-V 子分区[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)到 PF 微型端口驱动程序。 在此 OID 请求中传递的参数包括 NIC 的标识符上分配 VF 切换。 其他参数包括 VF 会附加到的子分区的标识符。

    PF 微型端口驱动程序为 VF 分配所需的硬件和软件资源。 PF 微型端口驱动程序 PCIe 请求程序标识符 (RID) 还决定 VF 的上，通过调用[ **NdisMGetVirtualFunctionLocation**](https://msdn.microsoft.com/library/windows/hardware/hh451487)。 RID 用于 DMA 和中断重新映射 DMA 请求时，中断生成的取景器。

    已成功完成时由 PF 微型端口驱动程序返回 VF 标识符以及 RID [OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)请求。

    有关 VF 的资源分配的详细信息，请参阅[虚函数的分配资源](allocating-resources-for-a-virtual-function.md)。

3.  通过发出 OID 方法请求的 NIC 交换机上的虚拟化堆栈创建 VPort [OID\_NIC\_切换\_创建\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451816)到 PF 微型端口驱动程序。 在此 OID 请求中传递的参数包括 NIC 交换机的标识符在其上 VPort 创建。 其他参数包括的 VF VPort 将附加到的标识符。

    **请注意**VPort NIC 交换机上的始终存在，以及附加到 PF.的默认值 仅单个非默认可以创建并附加到 VF VPort。

    NDIS OID 将请求转发到 PF 微型端口驱动程序之前，它会分配是唯一的网络适配器上的有效 VPort 标识符。

    PF 微型端口驱动程序在处理时 OID 请求，它分配 VPort 所需的硬件资源，并为 VPort 保留标识符。 在更高版本的 OID 请求和 SR-IOV 函数调用中使用此标识符。

    有关如何创建 VPort 的详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

4.  不久后 VF 和 VPort 分配，可能会启动 HYPER-V 子分区。 在此期间，来宾操作系统中的网络组件通过发送和接收数据包的综合数据路径。 这包括数据包流量通过附加到 PF.VPort 的默认值 桥接子分区的流量，虚拟化堆栈将默认 VPort 配置与媒体访问控制 (MAC) 和子分区的 VM 网络适配器的虚拟 LAN (VLAN) 筛选器。

    后资源分配的 VF 和 VPort，虚拟化堆栈颁发的 OID 方法请求[OID\_接收\_筛选器\_移动\_筛选器](https://msdn.microsoft.com/library/windows/hardware/hh451845)到 PF 微型端口驱动程序. 此 OID 请求将从默认 VPort VM 网络适配器的 MAC 和 VLAN 的筛选器移到附加到 VF VPort。 这将导致与这些筛选器，以将它们转发到 VF VPort 通过 VF 数据路径匹配的数据包。

    **请注意**现有接收筛选器可能会从默认 VPort 到 VF VPort 使用移[OID\_接收\_筛选器\_移动\_筛选器](https://msdn.microsoft.com/library/windows/hardware/hh451845)。 此外，新的筛选器可能会使用上设置 VF VPort [OID\_接收\_筛选器\_设置\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569795)。

已成功创建 VF 和 VPort 和 VPort 上已经设置了 MAC 筛选器后，虚拟化堆栈会通知虚拟 PCI (VPCI) 虚拟服务提供商 (VSP)。 在管理操作系统的 HYPER-V 父分区中运行此 VSP。 此通知告诉 VPCI VSP，VF 成功分配并附加到子分区。 VPCI VSP 将通过虚拟机总线 (VMBus) 消息发送到在子分区的来宾操作系统中运行的 VPCI 虚拟服务客户端 (VSC)。 VPCI VSC 是公开 VF 网络适配器的 PCI 设备的总线驱动程序。

公开 VF 网络适配器后，在来宾操作系统中运行的即插即用子系统将检测到该适配器，并加载 VF 微型端口驱动程序。 此驱动程序注册到 NDIS。 已初始化 VF 微型端口驱动程序，并且 VF 网络适配器上配置了相应的数据包筛选器后，VF 数据路径是完全正常运行。 因此，来宾操作系统中的数据包流量切换到此数据路径综合数据路径中。