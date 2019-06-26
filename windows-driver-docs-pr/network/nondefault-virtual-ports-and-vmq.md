---
title: 非默认虚拟端口和 VMQ
description: 非默认虚拟端口和 VMQ
ms.assetid: 5F6F5378-2CA7-491D-953C-6F98B855B51A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 721b3b7b508dcb3547f4c4d7e883d7f9a97cb42f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354542"
---
# <a name="nondefault-virtual-ports-and-vmq"></a>非默认虚拟端口和 VMQ


默认 NIC 切换为支持单个根 I/O 虚拟化 (SR-IOV) 接口的网络适配器的一个组件。 该开关始终将默认虚拟端口 (VPort) 附加到 PCI Express (PCIe) 物理函数 (PF)。 此开关可以将一个或多个非默认 VPorts 附加到 PF. 有关详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

在管理操作系统的 HYPER-V 父分区中运行虚拟化堆栈。 此堆栈通过发出对象标识符 (OID) 的方法请求创建 VPorts [OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。 但是，在堆栈可以为通过 OID 方法请求的已分配的资源创建比 active PCIe 虚函数 (VFs) 数的更多 VPorts [OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

如果网络适配器上启用了 SR-IOV，必须禁用 VMQ 的全部功能。 但是，非默认的附加到 PF 和未附加到 VF VPorts 可以提供与虚拟机队列 (VMQ) 接口相同的功能。 以下几点讨论如何 VPorts 能够提供类似于 VMQ 的数据包传输的硬件加速数据路径：

-   VMQ 确定的目标 VM 的媒体访问控制 (MAC) 在硬件中进行筛选。 这避免了确定虚拟化堆栈中的目标 VM 的开销。

    从 Windows Server 2012 开始，虚拟化堆栈配置的接收筛选器上 VPort 通过发出的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter). 对于此 OID 请求中，虚拟化堆栈传递[ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，它指定 MAC 地址和虚拟LAN (VLAN) 与虚拟网络适配器相关联的标识符。 类似于 VMQ，它可以配置多个 MAC 地址和 VLAN ID 对 VPort 上。 虚拟化堆栈还指定了接收筛选器将设置为目标 VPort。

    SR-IOV 网络适配器执行基于通过指定筛选条件的类似硬件筛选[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)请求。 在硬件上接收数据包时接收队列 VPort、 微型端口驱动程序的带外 (OOB) 数据中指定的源 VPort 标识符[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)数据包的结构。 基于 VPort 标识符，虚拟化堆栈确定目标 VM，并指示在 VM 中运行的网络堆栈的数据包。

    同样，虚拟化堆栈的 OOB 数据中指定的目标 VPort 标识符[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)传输数据包的结构。 当驱动程序处理该数据包在发送请求时，它指定 VPort 的硬件传输队列中将该数据包。

    可以通过使用从数据包的 OOB 数据获取 VPort 标识符[ **NET\_缓冲区\_列表\_接收\_筛选器\_VPORT\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-vport-id)宏。

    有关此过程的详细信息，请参阅[数据包流经虚拟端口](packet-flow-over-a-virtual-port.md)。

    有关筛选要求的 SR-IOV 网络适配器的接收的详细信息，请参阅[确定收到的筛选功能](determining-receive-filtering-capabilities.md)。

-   VMQ 提供中断和 DPC 并发性。

    从 NDIS 6.30 和 Windows Server 2012 开始，可以对附加到 PF VPort 被配置为具有特定的 CPU 关联。 虚拟化堆栈情况下使用的 OID 方法请求针对 VPort 配置 CPU 关联和中断裁决参数[OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)或[OID\_NIC\_交换机\_VPORT\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)。 通过执行此操作，虚拟化堆栈配置基于中断的中断和 DPC 并发类似于 VMQ 的参数。

    例如，当 SR-IOV 网络适配器收到上被配置为具有特定的 CPU 关联 VPort 数据包时，适配器将生成指定 CPU 上的中断。 微型端口驱动程序指示该 CPU 到 NDIS 和虚拟化堆栈接收到的数据包。

PF 微型端口驱动程序播发到调用上下文中的其 SR-IOV 功能[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)。 该驱动程序初始化[ **NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构与它的功能和调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)来注册它的功能。 有关详细信息，请参阅[确定的 SR-IOV 功能](determining-sr-iov-capabilities.md)。

以下成员[ **NDIS_NIC_SWITCH_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构会影响分配 VPorts 的方式：

-   **MaxNumVPorts**，它指定可以在网络适配器创建的 VPorts 的最大数目。

-   **MaxNumVFs**，其中网络适配器上指定可以分配的 VFs 的最大数目。

从 NDIS 6.30 开始，当微型端口驱动程序初始化[ **NDIS_NIC_SWITCH_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构，它可以设置 NDIS\_NIC\_开关\_CAPS\_单个\_VPORT\_中的池标志**NicSwitchCapabilities**成员。 此标志指定非默认 VPorts 可以创建从网络适配器上的 VPort 池未预留的方式。 这允许提供非默认 VPorts 创建并基于根据需要分配到 PF 和分配 VFs。 如果 VMQ 接口，非默认分配给 PF VPorts 还可以为 VM 使用此网络适配器支持接收队列。

如果 NDIS\_NIC\_交换机\_CAP\_单个\_VPORT\_池标志是设置此选项，提供非默认，VPorts 被创建并分配给 PF 并分配 VFs。 VPorts，可以创建并分配给 PF 的最大数目是相同的值，该驱动程序中的报表**MaxNumVPorts**成员。 微型端口驱动程序必须保留一个 VPort 要用作默认值分配给 PF.VPort 因此，非默认 VPorts，可以分配给 PF 并用于 VM 的最大数目接收队列是 (**MaxNumVPorts**– 1)。

> [!NOTE]
> 如果设置此标志，创建和分配的非默认 VPorts 不保留 VF 分配。 因此，其中取景器可能无法分配 VPort 如果池已耗尽可用 VPorts 的情况下可能会发生。 

如果 NDIS\_NIC\_交换机\_CAP\_单个\_VPORT\_池标志不是组、 创建和分配的非默认为 VF 分配保留 VPorts。 其他非默认 VPorts，可以创建和分配给 PF 并用于 VM 的最大数目接收队列是 (**MaxNumVPorts**–**MaxNumVFs**)。

有关 VMQ 的详细信息，请参阅[虚拟机队列 (VMQ)](virtual-machine-queue--vmq-.md)。
