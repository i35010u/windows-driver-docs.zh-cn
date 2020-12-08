---
title: 虚拟功能初始化序列
description: 虚拟功能初始化序列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ddf418e9b4550ec8352a49f38fff023dabb2f17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802270"
---
# <a name="virtual-function-initialization-sequence"></a>虚拟功能初始化序列


支持 (SR-IOV) 的单个根 i/o 虚拟化的网络适配器必须能够支持以下硬件组件：

-   一个 PCI Express (PCIe) 物理功能 (PF) 。 PF 始终存在于网络适配器上，并附加到 Hyper-v 父分区。

    有关此硬件组件的详细信息，请参阅 [Sr-iov 物理 Function (PF) ](sr-iov-physical-function--pf-.md)。

-   一个或多个 PCIe 虚拟功能 (VF) 。 必须将每个 VF 初始化并附加到 Hyper-v 子分区，来宾操作系统的网络组件才能通过 VF 发送或接收数据包。

    有关此硬件组件的详细信息，请参阅 [sr-iov)  (Sr-iov 虚拟函数 ](sr-iov-virtual-functions--vfs-.md)。

PF 微型端口驱动程序（在 Hyper-v 父分区的管理操作系统中运行）为 SR-IOV 网络适配器上的 VF 初始化并分配资源。 在 NDIS 调用 PF 微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数后，ndis 和虚拟化堆栈可以发出对象标识符 (OID) 请求发送到 PF 微型端口驱动程序，以执行以下操作：

-   在网络适配器上创建 NIC 交换机。 NIC 交换机将 VFs、PF 和物理网络端口间的网络流量桥接。

    有关详细信息，请参阅 [NIC 交换机](nic-switches.md)。

    **注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 *默认 NIC 交换机*，由 NDIS \_ 默认 \_ 交换机 \_ ID 标识符引用。



-   请求 PF 微型端口驱动程序，为网络适配器上的 VF 初始化和分配资源。

    有关详细信息，请参阅 [sr-iov)  (Sr-iov 虚拟函数 ](sr-iov-virtual-functions--vfs-.md)。

-   在 NIC 交换机上创建一个 (VPort) 的虚拟端口，并将其附加到 VF。

    有关详细信息，请参阅 [虚拟端口 (VPorts) ](virtual-ports--vports-.md)。

下图显示了与 VF 初始化相关的步骤。

![显示从虚拟化堆栈到 ndis 再到 pf 微型端口驱动程序的调用的示例 vf 初始化序列](images/sriov-vf-initialization.png)

在 VF 初始化序列过程中，NDIS、虚拟化堆栈和 PF 微型端口驱动程序会按照以下步骤进行操作：

1.  NDIS 从注册表读取默认的交换机配置，并发出 oid [ \_ NIC \_ 交换机 \_ CREATE \_ 交换机](./oid-nic-switch-create-switch.md) 的 oid 方法请求，以在网络适配器中设置交换机。 在此 OID 请求中传递的参数包括有关如何配置重要硬件资源（如 VFs 和 VPorts）的信息。 其中还包括有关如何在非默认 VPorts 和附加到 PF 的默认 VPort 之间分配资源的信息。

    在 PF 微型端口驱动程序成功完成 OID 后，可以使用 NIC 交换机创建 VPorts 并在其上分配 VFs。

    有关如何创建 NIC 交换机的详细信息，请参阅 [创建 Nic 交换机](creating-a-nic-switch.md)。

2.  VF 被视为虚拟机 (VM) 网络适配器的卸载机制。 此适配器在 Hyper-v 子分区中运行的来宾操作系统中公开。 默认情况下，来宾操作系统中的网络组件通过基于软件的合成数据路径发送和接收数据包。 但是，如果为 VF 卸载启用了子分区，则虚拟化堆栈会向该虚拟机的资源分配和初始化的 PF 小型端口驱动程序发出 OID 请求。 将 VF 附加到子分区并在 NIC 交换机上 VPort 后，网络组件将通过 VF 数据路径发送和接收数据包。 有关这些数据路径的详细信息，请参阅 [Sr-iov 数据路径](sr-iov-data-paths.md)。

    如果已为 VF 卸载启用了 Hyper-v 子分区，则虚拟化堆栈会发出 Oid NIC 交换机的 OID 方法请求，并将 [ \_ \_ \_ \_ VF 分配](./oid-nic-switch-allocate-vf.md) 到 PF 微型端口驱动程序。 在此 OID 请求中传递的参数包括分配有 VF 的 NIC 交换机的标识符。 其他参数包含 VF 将附加到的子分区的标识符。

    PF 微型端口驱动程序为 VF 分配必要的硬件和软件资源。 PF 端口驱动程序还通过调用 [**NdisMGetVirtualFunctionLocation**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionlocation)来确定 VF (RID) 的 PCIe 请求程序标识符。 当 VF 生成 DMA 请求和中断时，RID 用于 DMA 和中断重映射。

    当 "PF" 微型端口驱动程序成功完成 [OID \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md) 请求时，该 RID 连同 VF 标识符一起返回。

    有关 VF 的资源分配的详细信息，请参阅为 [虚拟函数分配资源](allocating-resources-for-a-virtual-function.md)。

3.  虚拟化堆栈通过向 PF 微型端口驱动程序发出 [oid \_ nic \_ switch \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md) 的 oid 方法请求，在 NIC 交换机上创建一个 VPort。 在此 OID 请求中传递的参数包括要在其上创建 VPort 的 NIC 交换机的标识符。 其他参数包括 VPort 将附加到的 VF 的标识符。

    **注意**  NIC 交换机上的默认 VPort 始终存在，并附加到 PF。 只能创建单个非默认 VPort，并将其附加到 VF。

    在 NDIS 将 OID 请求转发到 PF 微型端口驱动程序之前，它会分配一个在网络适配器上唯一的有效 VPort 标识符。

    当 PF 微型端口驱动程序处理 OID 请求时，它会分配 VPort 所需的硬件资源并保留 VPort 的标识符。 此标识符用于以后的 OID 请求和 SR-IOV 函数调用中。

    有关如何创建 VPort 的详细信息，请参阅 [创建虚拟端口](creating-a-virtual-port.md)。

4.  Hyper-v 子分区可能会在分配 VF 和 VPort 之前启动一段时间。 在此期间，来宾操作系统中的网络组件通过合成数据路径发送和接收数据包。 这涉及连接到 PF 的默认 VPort 上的数据包流量。 若要将流量桥接到子分区，虚拟化堆栈会将默认 VPort 配置为具有子分区 VM 网络适配器的媒体访问控制 (MAC) 和虚拟 LAN (VLAN) 筛选器。

    分配用于 VF 和 VPort 的资源后，虚拟化堆栈发出 oid [ \_ 接收 \_ 筛选器 \_ 将 \_ 筛选器移动筛选器](./oid-receive-filter-move-filter.md) 的 oid 方法请求发送到 PF 微型端口驱动程序。 此 OID 请求将 VM 网络适配器的 MAC 和 VLAN 筛选器从默认 VPort 移动到附加到 VF 的 VPort。 这会导致与这些筛选器相匹配的数据包通过 VF 数据路径转发到 VF VPort。

    **注意**  可以使用 [OID \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器](./oid-receive-filter-move-filter.md)将现有接收筛选器从默认 VPort 移动到 VF VPort。 此外，还可以通过使用 [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)在 VF VPort 上设置新的筛选器。

成功创建 VF 和 VPort 并在 VPort 上设置 MAC 筛选器后，虚拟化堆栈会) 虚拟服务提供商 (VSP) 通知虚拟 PCI (。 此 VSP 在 Hyper-v 父分区的管理操作系统中运行。 通知会通知 VPCI VSP 已成功分配并附加到子分区的 VF。 VPCI VSP 通过虚拟机总线将消息发送 (VMBus) 到子分区来宾操作系统中运行的 VPCI virtual service client (VSC) 。 VPCI VSC 是一种总线驱动程序，用于为 VF 网络适配器公开 PCI 设备。

公开 VF 网络适配器后，在来宾操作系统中运行的 PnP 子系统将检测适配器并加载 VF 微型端口驱动程序。 此驱动程序注册到 NDIS。 初始化 VF 微型端口驱动程序并在 VF 网络适配器上配置相应的数据包筛选器后，VF 数据路径将完全正常运行。 因此，来宾操作系统中的数据包流量从合成数据路径切换到此数据路径。
