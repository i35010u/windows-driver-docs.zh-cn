---
title: 虚拟端口 (VPort)
description: 虚拟端口 (VPort)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d152ff2ce2576c0aa70e9146039beb500040d25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805133"
---
# <a name="virtual-ports-vports"></a>虚拟端口 (VPort)


虚拟端口 (VPort) 为数据对象，该对象表示网络适配器的 NIC 交换机上的内部端口，该网络适配器支持 (SR-IOV) 的单一根 i/o 虚拟化。 每个 NIC 交换机都具有以下用于网络连接的端口：

-   一个外部物理端口，用于连接到外部物理网络。

-   一个或多个内部 VPorts 连接到 PCI Express 物理函数 (PF) 或虚函数 (VFs) 。

    PF 连接到 Hyper-v 父分区，并作为在该分区中运行的管理操作系统中的虚拟网络适配器公开。

    VF 附加到 Hyper-v 子分区，并作为在该分区中运行的来宾操作系统中的虚拟网络适配器公开。

NIC 交换机将物理端口的网络流量桥接到一个或多个 VPorts。 这将提供对基础物理网络接口的虚拟化访问。

每个 VPort 都具有唯一的标识符 (*VPortId*) ，该标识符对于网络适配器上的 NIC 交换机是唯一的。 默认的 NIC 交换机上始终存在一个默认的 VPort，并且永远不能删除。 默认的 VPort 具有 NDIS \_ 默认 \_ VPort ID 的 VPortId \_ 。

当 PF 微型端口驱动程序处理 [oid \_ NIC \_ 交换机 \_ CREATE \_ SWITCH](./oid-nic-switch-create-switch.md)) 方法请求 (的对象标识符时，它将为该交换机创建 NIC 交换机和默认 VPort。 默认 VPort 始终附加到 PF，并始终处于操作状态。

非默认 VPorts 是通过 oid [ \_ NIC \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 方法请求创建的。 只能将一个非默认的 VPort 附加到 VF。 附加后，默认值将处于操作状态。 还可以创建一个或多个非默认 VPorts，并将其附加到 PF。 这些 VPorts 在创建时 nonoperational，并可通过 oid [ \_ NIC \_ 交换机 \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md)的 oid 集请求运行。

**注意**  在 VPort 变为可操作后，仅当通过 oid [ \_ NIC \_ SWITCH \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md)的 oid 请求删除时，才能变成 nonoperational。



每个 VPort 都有一个或多个与之关联的硬件队列对，用于接收和传输数据包。 默认的 VPort 将保留网络适配器上的默认队列对。 在通过 [OID \_ NIC \_ 交换机 \_ CREATE \_ VPort](./oid-nic-switch-create-vport.md) 请求创建 VPort 时，将分配和分配用于非默认 VPorts 的队列对。

默认的 VPorts 是通过 oid [ \_ NIC \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 方法请求创建和配置的。 默认的 VPort 和非默认 VPorts 通过 oid [ \_ NIC \_ SWITCH \_ VPort \_ 参数](./oid-nic-switch-vport-parameters.md)的 oid 设置请求进行重新配置。 每个 OID 请求都包含一个用于指定以下配置参数的 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构：

-   VPort 附加到的 PCIe 函数。

    每个 VPort 可随时附加到 PF 或使用 VF。 创建 VPort 并将其附加到 PCIe 函数后，无法将附件动态更改为其他 PCIe 函数。

    **注意**  默认 VPort 始终连接到网络适配器上的 PF。




从 Windows Server 2012 中的 NDIS 6.30 开始，只能将一个非默认的 VPort 附加到 VF。 但是，可以将多个非默认 VPorts 连同默认 VPort 一起附加到 PF。


-   分配给 VPort 的硬件队列对数。

    每个 VPort 都有一组可供其使用的硬件队列对。 每个队列对由网络适配器上的单独传输队列和接收队列组成。

    队列对是网络适配器上的有限资源。 默认情况下，将在创建 NIC 交换机时指定默认和非默认 VPorts 使用的队列对总数。 这允许分配给默认 VPort 的队列对数不同于非默认的 VPorts。

    每个非默认 VPort 可以配置为具有不同的队列对数。 这称为队列对的 *非对称分配* 。 如果 NIC 不允许这样的非对称分配，则每个非默认 VPort 将配置为具有相同数量的队列对。 这称为队列对的 *对称分配* 。 有关详细信息，请参阅 [队列对的对称和非对称分配](symmetric-and-asymmetric-assignment-of-queue-pairs.md)。

    **注意**  PF 微型端口驱动程序报告在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)期间是否支持队列对的非对称分配。 有关详细信息，请参阅 [初始化 PF 微型端口驱动程序](initializing-a-pf-miniport-driver.md)。




分配给每个 VPort 的队列对数不会动态更改。 创建 VPort 后，不能更改分配给 VPort 的队列对的数目。

**注意**  分配给非默认 VPorts 的一个或多个队列对可用于在来宾操作系统中运行的 VF 微型端口驱动程序 (RSS) 的接收方缩放。




-   VPort 的中断裁决参数。

    可以为不同的 VPorts 指定不同的中断裁决类型。 这允许虚拟化堆栈控制特定 VPort 生成的中断数。

除了配置参数外，过量驱动程序还可以通过发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求，为每个 VPort 配置接收筛选器。 NIC 交换机按 VPort 执行指定的接收筛选。

接收筛选器的 VPorts 参数包括数据包筛选条件，如媒体访问控制列表 (MAC) 地址和虚拟 LAN (VLAN) 标识符。 MAC 地址和 VLAN 标识符的筛选器始终在与 [OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md)器请求关联的 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)中一起指定。 NIC 交换机必须将传入数据包筛选到其目标 MAC 地址和 VLAN 标识符与 VPort 上设置的任何接收筛选条件匹配的交换机。 NIC 交换机筛选从另一个 VPort 或外部物理端口接收的数据包。 如果数据包与筛选器匹配，则 NIC 交换机必须将其转发到 VPort。

可以在 VPort 上设置多个 MAC 地址和 VLAN 标识符对。 如果仅设置 MAC 地址，则接收筛选器指定 VPort 应收到与以下条件匹配的数据包：

-   数据包的目标 MAC 地址与筛选器的 MAC 地址相匹配。

-   如果 vlan 标记) VLAN 标识符为零时，则数据包有 VLAN 标记或 (。

默认的 VPorts 通过 oid [ \_ NIC \_ 交换机 \_ DELETE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 集请求删除。 仅当通过 oid [ \_ nic \_ 交换机 \_ 删除 \_ 开关](./oid-nic-switch-delete-switch.md)的 oid 设置请求删除 NIC 交换机时，才会删除默认 VPort。
