---
title: 创建虚拟端口
description: 创建虚拟端口
ms.assetid: 6102576D-3236-4FDD-8963-83A9E90FF7F0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e1ff8fedc40772c12b391c94137644874c7131b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838161"
---
# <a name="creating-a-virtual-port"></a>创建虚拟端口


虚拟端口（VPort）是一个数据对象，表示支持单一根 i/o 虚拟化（SR-IOV）的网络适配器的 NIC 交换机上的内部端口。 每个 NIC 交换机都具有以下用于网络连接的端口：

-   一个外部物理端口，用于连接到外部物理网络。

-   一个或多个与 PCI Express （PCIe）物理功能（PF）或虚拟函数（VFs）连接的内部 VPorts。

    PF 连接到 Hyper-v 父分区，并作为在该分区中运行的管理操作系统中的虚拟网络适配器公开。

    VF 附加到 Hyper-v 子分区，并作为在该分区中运行的来宾操作系统中的虚拟网络适配器公开。

有两种类型的 VPorts：

<a href="" id="default-vport"></a>默认 VPort  
默认 VPort 提供到在管理操作系统中运行的网络组件的网络连接。 默认的 VPort 的标识符\_默认\_VPORT\_ID。

当 PF 微型端口驱动程序创建和配置默认 NIC 交换机时，驱动程序将隐式创建默认的 VPort，并将其附加到 PF。 默认 VPort 不能附加到 VF。

默认 VPort 始终处于激活状态，无法显式删除。 仅当删除默认 NIC 交换机时，PF 微型端口驱动程序才会隐式删除默认 VPort。

有关如何在交换机上创建 NIC 交换机和默认 VPort 的详细信息，请参阅[创建 Nic 交换机](creating-a-nic-switch.md)。

<a href="" id="nondefault-vport"></a>非默认 VPort  
创建 NIC 交换机时不会隐式创建非默认 VPorts。 覆盖的驱动程序（如虚拟化堆栈）通过发出 oid [\_NIC\_SWITCH\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)的 oid 方法请求来显式创建这些端口。 非默认 VPorts 可以连接到 PF 或 VF，只能在创建 NIC 交换机之后创建。

附加到 VF 的非默认 VPort 提供与来宾操作系统中运行的网络组件之间的网络连接。 创建并附加到 VF 后，非默认的 VPort 处于激活状态。

附加到 PF 的非默认 VPort 为在管理操作系统中运行的网络组件提供额外的网络卸载功能。 例如，PF 上的非默认 VPorts 可以用于提供类似于虚拟机队列（VMQ）接口的卸载功能。

**注意** 只有在创建了 NIC 交换机之后，才能创建非默认 VPorts。



过量驱动程序发出 OID\_\_的对象标识符（OID）方法请求， [\_create\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport) ，在指定的 NIC 交换机上创建非默认的 VPORT。 此 OID 请求还会将创建的 VPort 附加到网络适配器的 PF 或之前分配的 VF。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_SWITCH\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。 成功从[OID 返回\_nic\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)请求之后， **NDIS\_NIC**的**VPORTID**成员\_\_的 VPORT\_参数结构具有VPort 标识符，在 NIC 交换机上的 VPorts 中是唯一的。

覆盖驱动程序将[**NDIS\_NIC 初始化\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构，以及有关要创建的非默认 VPORT 的配置信息。 配置信息包括非默认 VPort 附加到的 PCIe 函数以及非默认 VPort 的队列对数。

当初始化[**NDIS\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构时，过量驱动程序必须执行以下操作：

-   必须将**SwitchId**成员设置为先前在网络适配器上创建的 nic 交换机的标识符，该交换机通过 OID [\_nic\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)的 oid 方法请求来创建。

    **注意** 从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 "*默认 NIC 交换机*"。 创建非默认的 VPort 时，过量驱动程序必须将**SwitchId**成员设置为 NDIS\_默认\_交换机\_ID 标识符。



-   **VPortId**成员必须设置为 NDIS\_默认\_VPORT\_ID。

-   **AttachedFunctionId**成员必须设置为要附加非默认 VPORT 的 VF 或 PF 的标识符。

    值为 NDIS\_PF\_函数\_ID 指定 PF。 否则，必须将该值设置为一个 VF 的标识符，此 VF 的资源以前已通过 oid 的 OID 方法请求（ [\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)）进行了分配。

    **注意** 创建非默认 VPort 后，不能更改非默认 VPort 到 VF 或 PF 的附件。



过量驱动程序还可以指定分配给 VPort 的队列对数。 队列对是分配给 VPort 的网络适配器上的传输和接收队列。 如果网络适配器支持非默认 VPorts 的非对称队列对，则过量驱动程序可能会为驱动程序创建的每个 VPort 指定不同数量的队列对。 有关详细信息，请参阅[队列对的对称和非对称分配](symmetric-and-asymmetric-assignment-of-queue-pairs.md)。

过量驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)来[\_\_NIC 发出 OID，\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)请求到基础 PF 微型端口驱动程序。 在 NDIS 将 OID 方法请求转发到微型端口驱动程序之前，它将执行以下操作：

1.  NDIS 验证[**ndis\_NIC\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构中的参数。 如果参数错误，NDIS 将失败 OID 方法请求，且不会将请求传递到 PF 微型端口驱动程序。

2.  NDIS 为非默认 VPort 分配一个标识符，范围为从1到（**NumVPorts**–1）的范围内，其中**NumVPorts**是小型端口驱动程序在网络适配器上配置的 VPorts 的数目。 驱动程序在 NDIS\_NIC 的**NumVPorts**成员中指定此数字[ **\_交换机\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。 驱动程序通过 oid [\_NIC\_交换机\_枚举\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)来返回此结构。

    **注意** NDIS\_默认\_VPORT\_ID 的 VPort 标识符是为附加到默认 NIC 交换机上的 PF 的默认 VPort 预留的。




分配的 VPort 标识符唯一标识网络适配器的 NIC 交换机上的非默认的 VPort。


3.  NDIS 将 NDIS\_NIC 的**VPortId**成员设置\_交换机\_VPORT\_参数结构与分配的 VPORT 标识符。

当对 PF 小型端口驱动程序发出 OID 请求时，驱动程序会分配与指定的非默认 VPort 关联的硬件和软件资源。 成功分配所有资源后，PF 微型端口驱动程序会通过从[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)返回 NDIS\_\_状态，成功完成 OID。

如果[OID\_NIC\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)请求已成功完成，则 PF 微型端口驱动程序和过量驱动程序必须保留非默认 VPORT 的**VPortId**值才能执行后续操作。 在以下操作过程中将使用**VPortId**值：

-   NDIS 和过量驱动程序使用**VPortId**值标识与此 VPort 相关的后续 OID 请求中的非默认 VPort，如[oid\_nic\_SWITCH\_VPort\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)和[OID\_NIC\_交换机\_DELETE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)。

-   在发送操作期间，NDIS 指定**VPortId**值以标识从中发送数据包的 VPort。 此值在带外（OOB） [**NDIS\_NET\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)中指定，\_筛选[网络\_缓冲区\_列表](net-buffer-list-structure.md)结构的\_信息数据。

-   在接收操作期间，PF 微型端口驱动程序指定将数据包转发到的**VPortId**值。 此值还在 OOB [**NDIS\_NET\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)中指定，\_筛选[网络\_缓存\_列表](net-buffer-list-structure.md)结构\_信息数据。

以下几点适用于创建非默认 VPorts：

-   创建媒体访问控制（MAC）和虚拟 LAN （VLAN）标识符时，将在 VPort 上配置接收筛选器。 过量驱动程序通过颁发 oid [\_接收\_FILTER\_集\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)来动态设置这些接收筛选器。 还可以通过 OID [\_接收\_筛选器\_MOVE\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-move-filter)，将接收筛选器从一个 VPort 移到另一个。

-   附加到 VF 的非默认 VPort 在创建时处于激活状态。 如果 VPort 附加到 VF，则无法将其停用。

    创建时，附加到 PF 的非默认 VPort 处于停用状态。 在成功创建 VPort 后，生成的驱动程序（如 Hyper-v 可扩展交换机模块）会显式激活附加到 PF 的非默认 VPort。 这是通过以下方式实现的： [\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)发出 oid 方法请求，\_将\_参数发送到 PF 微型端口驱动程序。

    当过量驱动程序发出此 OID 请求时，它会将[**NDIS\_NIC 传递\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构，并将**VPortState**成员设置为**NdisNicSwitchVPortStateActivated**。

    在非默认 VPort 处于激活状态后，PF 微型端口驱动程序可以通过调用[**NdisAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatesharedmemory)为 VPort 分配共享内存。 驱动程序必须将[**NDIS\_共享\_内存\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)结构中的**VPortId**成员设置为 VPort 的标识符值。

**注意** 当非默认的 VPort 处于激活状态时，仅当通过 oid 的 oid 集请求[\_NIC\_开关\_DELETE\_VPort](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)时，才会将其设置为 "已停用" 状态。











