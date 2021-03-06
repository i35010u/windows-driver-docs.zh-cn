---
title: 非默认虚拟端口和 VMQ
description: 非默认虚拟端口和 VMQ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6929b6c97a7e86872fb9c886bfe5a972ad386dfd
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248696"
---
# <a name="nondefault-virtual-ports-and-vmq"></a>非默认虚拟端口和 VMQ


默认 NIC 交换机是网络适配器的一个组件，它支持 (SR-IOV) 接口的单个根 i/o 虚拟化。 开关始终将 (VPort) 的默认虚拟端口附加到 PCI Express (PCIe) 物理函数 (PF) 。 开关可以将一个或多个非默认 VPorts 附加到 PF。 有关详细信息，请参阅 [创建虚拟端口](creating-a-virtual-port.md)。

虚拟化堆栈在 Hyper-v 父分区的管理操作系统中运行。 此堆栈 (OID [ \_ NIC \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid) 方法请求发出对象标识符来创建 VPorts。 但是，堆栈可能会创建比 (VFs) 的活动 PCIe 虚拟函数数更多的 VPorts，这些函数通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 oid 方法请求分配了资源。

如果在网络适配器上启用了 SR-IOV，则必须禁用全部 VMQ 功能。 但是，附加到 PF 且未附加到 VF 的非默认 VPorts 可以提供与虚拟机队列相同的功能 (VMQ) 接口。 以下几点讨论了 VPorts 如何为数据包传输提供硬件加速的数据路径，这与 VMQ 类似：

-   VMQ 通过 media access control 确定目标 VM (MAC) 在硬件中进行筛选。 这样可以避免在虚拟化堆栈中确定目标 VM 的开销。

    从 Windows Server 2012 开始，虚拟化堆栈通过发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)发出 oid 方法请求，在 VPort 上配置接收筛选器。 对于此 OID 请求，虚拟化堆栈会传递 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构，该结构指定与虚拟网络适配器关联的 MAC 地址和虚拟 LAN (VLAN) 标识符。 与 VMQ 类似，它可以在 VPort 上配置多个 MAC 地址和 VLAN ID 对。 虚拟化堆栈还指定接收筛选器将设置到的目标 VPort。

    SR-IOV 网络适配器根据通过 [OID \_ 接收 \_ 筛选器 \_ 集 \_ ](./oid-receive-filter-set-filter.md) 请求指定的筛选条件执行类似的硬件筛选。 在 VPort 的硬件接收队列中接收数据包时，微型端口驱动程序在带外 () OOB 中指定数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构的源 VPort 标识符。 根据 VPort 标识符，虚拟化堆栈确定目标 VM，并向 VM 中运行的网络堆栈指出数据包。

    同样，虚拟化堆栈指定传输数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构的 OOB 数据中的目标 VPort 标识符。 当驱动程序处理数据包的发送请求时，它会将数据包放在指定 VPort 的硬件传输队列中。

    可以通过使用 [**NET \_ BUFFER \_ LIST \_ RECEIVE \_ FILTER \_ VPORT \_ ID**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_receive_filter_vport_id) 宏从数据包的 OOB 数据中获取 VPort 标识符。

    有关此过程的详细信息，请参阅 [通过虚拟端口的数据包流](packet-flow-over-a-virtual-port.md)。

    有关 SR-IOV 网络适配器接收筛选要求的详细信息，请参阅 [确定接收筛选功能](determining-receive-filtering-capabilities.md)。

-   VMQ 提供中断和 DPC 并发。

    从 NDIS 6.30 和 Windows Server 2012 开始，可以将附加到 PF 的 VPort 配置为具有特定的 CPU 关联。 虚拟化堆栈使用 [oid \_ nic \_ switch \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md) 或 [oid \_ nic \_ switch \_ VPort \_ 参数](./oid-nic-switch-vport-parameters.md)的 oid 方法请求为 VPort 配置 CPU 关联和中断裁决参数。 这样，虚拟化堆栈就会为中断和 DPC 并发配置类似于 VMQ 的基于中断的参数。

    例如，当 SR-IOV 网络适配器在配置为具有特定 CPU 关联的 VPort 上接收数据包时，适配器将在指定 CPU 上生成中断。 微型端口驱动程序指示接收到 NDIS 的数据包和该 CPU 的虚拟化堆栈。

PF 微型端口驱动程序在对 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用的上下文中公布其 sr-iov 功能。 驱动程序使用其功能初始化 [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构并调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 来注册其功能。 有关详细信息，请参阅 [确定 Sr-iov 功能](determining-sr-iov-capabilities.md)。

[**NDIS_NIC_SWITCH_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构的以下成员会影响 VPorts 的分配方式：

-   **MaxNumVPorts**，指定可在网络适配器上创建的最大 VPorts 数。

-   **MaxNumVFs**，指定可在网络适配器上分配的最大 VFs 数。

从 NDIS 6.30 开始，当微型端口驱动程序初始化 [**NDIS_NIC_SWITCH_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构时，它可以 \_ \_ \_ 在 NicSwitchCapabilities 成员中设置 NDIS NIC 交换机 cap \_ 单一 \_ VPORT \_ 池标志。  此标志指定可以从网络适配器上的 VPort 池 nonreserved 的方式创建非默认 VPorts。 这允许按照所需的方式创建和分配可用的非默认 VPorts 到 PF 和分配的 VFs。 如果网络适配器支持 VMQ 接口，则分配到 PF 的非默认 VPorts 也可用于 VM 接收队列。

如果设置了 NDIS \_ NIC \_ 交换机 \_ cap \_ 单一 \_ VPORT \_ 池标志，则将创建可用的非默认 VPorts，并将其分配给 PF 并分配给 VFs。 可创建并分配到 PF 的最大 VPorts 数与驱动程序在 **MaxNumVPorts** 成员中报告的值相同。 微型端口驱动程序必须保留一个 VPort，以将其用作分配到 PF 的默认 VPort。 因此，可分配到 PF 并用于 VM 接收队列的非默认 VPorts 数量 (**MaxNumVPorts**– 1) 。

> [!NOTE]
> 如果设置了此标志，则不会为 VF 分配保留创建和分配非默认 VPorts。 因此，如果某个 VF 的可用 VPorts 用尽，则可能不会为 VF 分配 VPort。 

如果 \_ \_ 未设置 NDIS NIC 交换机 \_ cap \_ 单一 \_ VPORT \_ 池标志，则将为 VF 分配保留创建和分配非默认的 VPorts。 可创建并分配到 PF 并用于 VM 接收队列的其他非默认 VPorts 的最大数目为 (**MaxNumVPorts**–**MaxNumVFs**) 。

有关 VMQ 的详细信息，请参阅 [ (vmq) 虚拟机队列 ](virtual-machine-queue--vmq-.md)。
