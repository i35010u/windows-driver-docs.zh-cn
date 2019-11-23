---
title: 非默认虚拟端口和 VMQ
description: 非默认虚拟端口和 VMQ
ms.assetid: 5F6F5378-2CA7-491D-953C-6F98B855B51A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e2f09cfd9d19cb78bac6e7b5d536c128490c1ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842764"
---
# <a name="nondefault-virtual-ports-and-vmq"></a>非默认虚拟端口和 VMQ


默认 NIC 交换机是支持单根 i/o 虚拟化（SR-IOV）接口的网络适配器组件。 开关始终将默认的虚拟端口（VPort）附加到 PCI Express （PCIe）物理功能（PF）。 开关可以将一个或多个非默认 VPorts 附加到 PF。 有关详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

虚拟化堆栈在 Hyper-v 父分区的管理操作系统中运行。 此堆栈通过\_\_NIC 发出对象标识符（OID）方法请求来创建 VPorts， [\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。 但是，堆栈创建的 VPorts 超过活动 PCIe 虚拟函数（VFs）的数目，而这些功能是通过 oid\_NIC 的 oid 方法请求[\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

如果在网络适配器上启用了 SR-IOV，则必须禁用全部 VMQ 功能。 但是，附加到 PF 且未附加到 VF 的非默认 VPorts 可以提供与虚拟机队列（VMQ）界面相同的功能。 以下几点讨论了 VPorts 如何为数据包传输提供硬件加速的数据路径，这与 VMQ 类似：

-   VMQ 通过硬件中的媒体访问控制（MAC）筛选来确定目标 VM。 这样可以避免在虚拟化堆栈中确定目标 VM 的开销。

    从 Windows Server 2012 开始，虚拟化堆栈通过发出 oid [\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)来配置接收筛选器。 对于此 OID 请求，虚拟化堆栈会传递[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，该结构指定与虚拟网络适配器关联的 MAC 地址和虚拟 LAN （VLAN）标识符。 与 VMQ 类似，它可以在 VPort 上配置多个 MAC 地址和 VLAN ID 对。 虚拟化堆栈还指定接收筛选器将设置到的目标 VPort。

    SR-IOV 网络适配器根据通过 OID 指定的筛选条件[\_接收\_filter\_设置\_FILTER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)请求来执行类似的硬件筛选。 在 VPort 的硬件接收队列中接收数据包时，微型端口驱动程序会在[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的带外（OOB）数据中指定源 VPort 标识符，\_数据包的列表结构。 根据 VPort 标识符，虚拟化堆栈确定目标 VM，并向 VM 中运行的网络堆栈指出数据包。

    同样，虚拟化堆栈指定传输数据包的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 OOB 数据中的目标 VPort 标识符。 当驱动程序处理数据包的发送请求时，它会将数据包放在指定 VPort 的硬件传输队列中。

    可以使用 NET\_BUFFER\_列表从数据包的 OOB 数据中获取 VPort 标识符， [ **\_\_FILTER\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)宏。\_

    有关此过程的详细信息，请参阅[通过虚拟端口的数据包流](packet-flow-over-a-virtual-port.md)。

    有关 SR-IOV 网络适配器接收筛选要求的详细信息，请参阅[确定接收筛选功能](determining-receive-filtering-capabilities.md)。

-   VMQ 提供中断和 DPC 并发。

    从 NDIS 6.30 和 Windows Server 2012 开始，可以将附加到 PF 的 VPort 配置为具有特定的 CPU 关联。 虚拟化堆栈为 VPort 配置 CPU 关联和中断裁决参数，方法是使用 Oid\_NIC 的 OID 方法请求[\_交换机\_CREATE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)或[oid\_nic\_switch\_VPort\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)。 这样，虚拟化堆栈就会为中断和 DPC 并发配置类似于 VMQ 的基于中断的参数。

    例如，当 SR-IOV 网络适配器在配置为具有特定 CPU 关联的 VPort 上接收数据包时，适配器将在指定 CPU 上生成中断。 微型端口驱动程序指示接收到 NDIS 的数据包和该 CPU 的虚拟化堆栈。

PF 微型端口驱动程序在对[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用的上下文中公布其 sr-iov 功能。 驱动程序使用其功能初始化[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构，并调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)来注册其功能。 有关详细信息，请参阅[确定 Sr-iov 功能](determining-sr-iov-capabilities.md)。

[**NDIS_NIC_SWITCH_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构的以下成员会影响 VPorts 的分配方式：

-   **MaxNumVPorts**，指定可在网络适配器上创建的最大 VPorts 数。

-   **MaxNumVFs**，指定可在网络适配器上分配的最大 VFs 数。

从 NDIS 6.30 开始，当微型端口驱动程序对[**NDIS_NIC_SWITCH_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构进行初始化时，它可以设置 NDIS\_NIC\_交换机\_Cap\_**NicSwitchCapabilities**成员中的单个\_VPORT\_池标志。 此标志指定可以从网络适配器上的 VPort 池 nonreserved 的方式创建非默认 VPorts。 这允许按照所需的方式创建和分配可用的非默认 VPorts 到 PF 和分配的 VFs。 如果网络适配器支持 VMQ 接口，则分配到 PF 的非默认 VPorts 也可用于 VM 接收队列。

如果设置了 NDIS\_NIC\_交换机\_CAP\_单个\_VPORT\_池标志已设置，则将创建可用的非默认 VPorts，并将其分配给 PF 并分配给 VFs。 可创建并分配到 PF 的最大 VPorts 数与驱动程序在**MaxNumVPorts**成员中报告的值相同。 微型端口驱动程序必须保留一个 VPort，以将其用作分配到 PF 的默认 VPort。 因此，可分配到 PF 并用于 VM 接收队列的非默认 VPorts 数为（**MaxNumVPorts**–1）。

> [!NOTE]
> 如果设置此标志，则不会为 VF 分配保留创建和分配非默认 VPorts。 因此，如果某个 VF 的可用 VPorts 用尽，则可能不会为 VF 分配 VPort。 

如果未设置\_NIC\_交换机\_CAP\_单个\_VPORT\_池标志，则将为 VF 分配保留创建和分配非默认的 VPorts。 可创建并分配到 PF 并用于 VM 接收队列的其他非默认 VPorts 数为（**MaxNumVPorts**–**MaxNumVFs**）。

有关 VMQ 的详细信息，请参阅[虚拟机队列（VMQ）](virtual-machine-queue--vmq-.md)。
