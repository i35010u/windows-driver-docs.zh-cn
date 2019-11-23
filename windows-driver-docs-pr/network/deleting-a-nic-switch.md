---
title: 删除 NIC 交换机
description: 删除 NIC 交换机
ms.assetid: BCC6A38B-F25B-483A-B9FF-D6FF73F9B2F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9a5b494625a668b06e514a4401057ad3bcf33a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838166"
---
# <a name="deleting-a-nic-switch"></a>删除 NIC 交换机


支持单根 i/o 虚拟化（SR-IOV）的网络适配器必须能够删除 NIC 交换机。 只有 SR-IOV 适配器的 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序可以删除适配器上的 NIC 交换机。

**注意**  从 Windows Server 2012 中的 NDIS 6.30 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为*默认 NIC 交换机*，由 NDIS\_默认\_交换机\_ID 标识符引用。

 

在停止 PF 微型端口驱动程序之前，NDIS 会通过发出一个对象标识符（OID）\_\_NIC 的对象标识符（OID）集请求来删除 NIC 交换机[\_DELETE\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)。 [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向[**NDIS\_NIC 的指针\_交换机\_DELETE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)结构（指定要删除的交换机的标识符）。\_

NDIS 在发出 oid\_NIC 的 OID 集请求之前强制执行以下策略[\_交换机\_DELETE\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)到 PF 微型端口驱动程序：

-   NDIS 保证所有接收筛选器都已从 NIC 交换机上的默认和非默认虚拟端口（VPorts）中清除。 通过 oid [\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)来清除接收筛选器。

-   NDIS 保证先前已删除在交换机上创建的所有非默认虚拟端口（VPorts）。 VPorts 通过 oid [\_NIC\_交换机\_DELETE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)删除。

-   NDIS 保证附加到 NIC 交换机的所有 PCIe 虚拟功能（VFs）资源都已被释放。 通过 oid [\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 VFs。

当接收到 oid\_NIC 的 OID 方法请求时[\_交换机\_DELETE\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的软件资源。 但是，在调用[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，驱动程序只能释放 NIC 交换机的硬件资源。

    有关静态 NIC 交换机创建的详细信息，请参阅[静态创建 Nic 交换机](static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持动态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的硬件和软件资源。

    有关动态 NIC 交换机创建的详细信息，请参阅[动态创建 Nic 交换机](dynamic-creation-of-a-nic-switch.md)。

3.  如果 PF 微型端口驱动程序支持动态创建 NIC 交换机，并在网络适配器上删除了所有 NIC 交换机，则驱动程序必须通过调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)禁用适配器上的虚拟化。 若要禁用虚拟化，网络适配器必须将*EnableVirtualization*参数设置为 FALSE，将*NumVFs*参数设置为零。

    [**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)清除**NumVFs**成员，并且 VF 在网络适配器的 PF 的 PCIe 配置空间中的 sr-iov 扩展功能结构中**启用**位。

    **请注意**  如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则在调用[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，它必须仅调用[**NdisMEnableVirtualization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 。

     

 

 





