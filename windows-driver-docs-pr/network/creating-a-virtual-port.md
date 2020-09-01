---
title: 创建虚拟端口
description: 创建虚拟端口
ms.assetid: 6102576D-3236-4FDD-8963-83A9E90FF7F0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61443c4056a5ae06640fa6987b271c87cd157ccc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214746"
---
# <a name="creating-a-virtual-port"></a>创建虚拟端口


 (VPort) 的虚拟端口是一个数据对象，表示网络适配器的 NIC 交换机上的一个内部端口，该网络适配器支持 (SR-IOV) 的单个根 i/o 虚拟化。 每个 NIC 交换机都具有以下用于网络连接的端口：

-   一个外部物理端口，用于连接到外部物理网络。

-   一个或多个内部 VPorts 连接到 PCI Express (PCIe) 物理功能 (PF) 或虚拟函数 (VFs) 。

    PF 连接到 Hyper-v 父分区，并作为在该分区中运行的管理操作系统中的虚拟网络适配器公开。

    VF 附加到 Hyper-v 子分区，并作为在该分区中运行的来宾操作系统中的虚拟网络适配器公开。

有两种类型的 VPorts：

<a href="" id="default-vport"></a>默认 VPort  
默认 VPort 提供到在管理操作系统中运行的网络组件的网络连接。 默认 VPort 具有 NDIS \_ default VPort ID 的标识符 \_ \_ 。

当 PF 微型端口驱动程序创建和配置默认 NIC 交换机时，驱动程序将隐式创建默认的 VPort，并将其附加到 PF。 默认 VPort 不能附加到 VF。

默认 VPort 始终处于激活状态，无法显式删除。 仅当删除默认 NIC 交换机时，PF 微型端口驱动程序才会隐式删除默认 VPort。

有关如何在交换机上创建 NIC 交换机和默认 VPort 的详细信息，请参阅 [创建 Nic 交换机](creating-a-nic-switch.md)。

<a href="" id="nondefault-vport"></a>非默认 VPort  
创建 NIC 交换机时不会隐式创建非默认 VPorts。 过量驱动程序（例如虚拟化堆栈）通过发出 [oid \_ NIC \_ SWITCH \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 方法请求来显式创建这些端口。 非默认 VPorts 可以连接到 PF 或 VF，只能在创建 NIC 交换机之后创建。

附加到 VF 的非默认 VPort 提供与来宾操作系统中运行的网络组件之间的网络连接。 创建并附加到 VF 后，非默认的 VPort 处于激活状态。

附加到 PF 的非默认 VPort 为在管理操作系统中运行的网络组件提供额外的网络卸载功能。 例如，PF 上的非默认 VPorts 可以用于提供类似于虚拟机队列 (VMQ) 接口的卸载功能。

**注意**  只有在创建了 NIC 交换机之后，才能创建非默认 VPorts。



过量驱动程序发出对象标识符)  (oid [ \_ NIC \_ 交换机 \_ create \_ VPORT](./oid-nic-switch-create-vport.md) 在指定的 NIC 交换机上创建非默认的 VPORT。 此 OID 请求还会将创建的 VPort 附加到网络适配器的 PF 或之前分配的 VF。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构的指针。 成功从[OID \_ nic \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)请求返回后， **NDIS \_ nic \_ 交换机 \_ VPORT \_ 参数**结构的**VPortId**成员具有一个 VPORT 标识符，该标识符在 NIC 交换机上的 VPorts 中是唯一的。

过量驱动程序将 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构初始化为有关要创建的非默认 VPORT 的配置信息。 配置信息包括非默认 VPort 附加到的 PCIe 函数以及非默认 VPort 的队列对数。

当初始化 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构时，过量驱动程序必须执行以下操作：

-   **SwitchId**成员必须设置为先前通过 oid [ \_ nic \_ 交换机 \_ CREATE \_ switch](./oid-nic-switch-create-switch.md)的 oid 方法请求在网络适配器上创建的 NIC 交换机的标识符。

    **注意**  从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 " *默认 NIC 交换机*"。 创建非默认的 VPort 时，过量驱动程序必须将 **SwitchId** 成员设置为 NDIS \_ 默认 \_ 交换机 \_ ID 标识符。



-   **VPortId**成员必须设置为 NDIS \_ DEFAULT \_ VPORT \_ ID。

-   **AttachedFunctionId**成员必须设置为要附加非默认 VPORT 的 VF 或 PF 的标识符。

    NDIS \_ PF \_ 函数 ID 的值 \_ 指定 PF。 否则，必须将该值设置为一个 VF 的标识符，此 VF 的资源以前通过 oid [ \_ NIC \_ 开关 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 oid 方法请求进行了分配。

    **注意**  创建非默认 VPort 后，不能更改非默认 VPort 到 VF 或 PF 的附件。



过量驱动程序还可以指定分配给 VPort 的队列对数。 队列对是分配给 VPort 的网络适配器上的传输和接收队列。 如果网络适配器支持非默认 VPorts 的非对称队列对，则过量驱动程序可能会为驱动程序创建的每个 VPort 指定不同数量的队列对。 有关详细信息，请参阅 [队列对的对称和非对称分配](symmetric-and-asymmetric-assignment-of-queue-pairs.md)。

过量驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 将 [OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md) 请求发送到基础 PF 微型端口驱动程序。 在 NDIS 将 OID 方法请求转发到微型端口驱动程序之前，它将执行以下操作：

1.  NDIS 验证 [**ndis \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构中的参数。 如果参数错误，NDIS 将失败 OID 方法请求，且不会将请求传递到 PF 微型端口驱动程序。

2.  NDIS 为非默认 VPort 分配一个标识符，范围为1到 (**NumVPorts**– 1) ，其中 **NumVPorts** 是在网络适配器上配置了微型端口驱动程序的 VPorts 的数目。 驱动程序在[**NDIS \_ NIC \_ 交换机 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构的**NumVPorts**成员中指定此编号。 驱动程序通过 oid [ \_ NIC \_ 交换机 \_ 枚举 \_ 开关](./oid-nic-switch-enum-switches.md)的 oid 查询请求返回此结构。

    **注意** \_ \_ \_ 对于附加到默认 NIC 交换机上的 PF 的默认 VPort，将保留 NDIS 默认 VPort ID 的 VPort 标识符。




分配的 VPort 标识符唯一标识网络适配器的 NIC 交换机上的非默认的 VPort。


3.  NDIS **VPortId** \_ \_ \_ \_ 用分配的 VPORT 标识符设置 ndis NIC 交换机 VPORT 参数结构的 VPortId 成员。

当对 PF 小型端口驱动程序发出 OID 请求时，驱动程序会分配与指定的非默认 VPort 关联的硬件和软件资源。 成功分配所有资源后，PF 微型端口驱动程序会通过 \_ 从 MiniportOidRequest 返回 NDIS 状态成功完成 OID \_ 。 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

如果 [OID \_ NIC \_ 交换机 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md) 请求成功完成，则 PF 微型端口驱动程序和过量驱动程序必须保留非默认 VPORT 的 **VPortId** 值，以便执行后续操作。 在以下操作过程中将使用 **VPortId** 值：

-   NDIS 和过量驱动程序使用 **VPortId** 值标识与此 VPort 相关的后续 oid 请求中的非默认 VPort，如 [oid \_ nic \_ switch \_ VPort \_ 参数](./oid-nic-switch-vport-parameters.md) 和 [oid \_ nic \_ switch \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md)。

-   在发送操作期间，NDIS 指定 **VPortId** 值以标识从中发送数据包的 VPort。 此值在带外 (OOB) [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info) 数据的 [网络 \_ 缓冲区 \_ 列表](net-buffer-list-structure.md) 结构内指定。

-   在接收操作期间，PF 微型端口驱动程序指定将数据包转发到的 **VPortId** 值。 此值还在[网络 \_ 缓冲区 \_ 列表](net-buffer-list-structure.md)结构的 OOB [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)数据中指定。

以下几点适用于创建非默认 VPorts：

-   在创建 VPort 后，将在上配置媒体访问控制 (MAC) 和虚拟 LAN (VLAN) 标识符的接收筛选器。 过量驱动程序通过发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求，动态设置这些接收筛选器。 还可以通过 oid 设置 [oid \_ 接收 \_ 筛选器 \_ 移动 \_ 筛选器](./oid-receive-filter-move-filter.md)将接收筛选器从一个 VPort 移到另一个。

-   附加到 VF 的非默认 VPort 在创建时处于激活状态。 如果 VPort 附加到 VF，则无法将其停用。

    创建时，附加到 PF 的非默认 VPort 处于停用状态。 在成功创建 VPort 后，生成的驱动程序（如 Hyper-v 可扩展交换机模块）会显式激活附加到 PF 的非默认 VPort。 完成此操作的方法是：将 [oid \_ NIC \_ SWITCH \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md) 的 oid 方法请求发送到 PF 微型端口驱动程序。

    当过量驱动程序发出此 OID 请求时，它会将[**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构传递到**NdisNicSwitchVPortStateActivated**的**VPortState**成员。

    在非默认 VPort 处于激活状态后，PF 微型端口驱动程序可以通过调用 [**NdisAllocateSharedMemory**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)为 VPort 分配共享内存。 驱动程序必须将[**NDIS \_ SHARED \_ MEMORY \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)结构中的**VPortId**成员设置为 VPort 的标识符值。

**注意**  当非默认 VPort 处于激活状态时，仅当通过 oid [ \_ NIC \_ SWITCH \_ DELETE \_ VPort](./oid-nic-switch-delete-vport.md)的 oid 集请求删除时，它才设置为已停用状态。