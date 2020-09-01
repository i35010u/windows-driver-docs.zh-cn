---
title: 删除 NIC 交换机
description: 删除 NIC 交换机
ms.assetid: BCC6A38B-F25B-483A-B9FF-D6FF73F9B2F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dc81155a7fdbd8cc7ccc8ebc040b80ea70c4bc7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211095"
---
# <a name="deleting-a-nic-switch"></a>删除 NIC 交换机


支持 (SR-IOV) 的单个根 i/o 虚拟化的网络适配器必须能够删除 NIC 交换机。 只有 PCI Express (PCIe) 物理功能 () PF 的微型端口驱动程序才能在该适配器上删除 NIC 交换机。

**注意**   从 Windows Server 2012 中的 NDIS 6.30 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 *默认 NIC 交换机*，由 NDIS \_ 默认 \_ 交换机 \_ ID 标识符引用。

 

在停止 PF 微型端口驱动程序之前，NDIS 会通过发出对象标识符 (OID 来删除 NIC 交换机) 设置 [oid \_ NIC \_ 交换机 \_ 删除 \_ 开关](./oid-nic-switch-delete-switch.md)。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指针，该指针指向用于指定要删除的交换机的标识符的[**ndis \_ NIC \_ 交换机 \_ 删除 \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_switch_parameters)结构。

在向 PF 微型端口驱动程序发出 [oid \_ NIC \_ 交换机 \_ 删除 \_ 开关](./oid-nic-switch-delete-switch.md) 的 oid 集请求之前，NDIS 强制执行以下策略：

-   NDIS 保证所有接收筛选器都已从默认和非默认虚拟端口中清除， (VPorts) 在 NIC 交换机上。 通过 oid 的 oid 集请求 [ \_ \_ \_ 清除 \_ 筛选器](./oid-receive-filter-clear-filter.md)清除接收筛选器。

-   NDIS 保证先前已删除在交换机上 (VPorts) 创建的所有非默认虚拟端口。 VPorts 通过 oid [ \_ NIC \_ 交换机 \_ DELETE \_ VPORT](./oid-nic-switch-delete-vport.md)的 oid 设置请求删除。

-   NDIS 可保证所有 PCIe 虚拟功能 (Vf) 的所有资源都已被释放。 通过 oid [ \_ NIC \_ 交换机 \_ 自由 \_ VF](./oid-nic-switch-free-vf.md)的 oid 集请求释放 VFs。

接收到 oid [ \_ NIC \_ 交换机 \_ 删除 \_ 开关](./oid-nic-switch-delete-switch.md)的 oid 方法请求时，PF 微型端口驱动程序必须执行以下操作：

1.  如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的软件资源。 但是，在调用 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 时，驱动程序只能释放 NIC 交换机的硬件资源。

    有关静态 NIC 交换机创建的详细信息，请参阅 [静态创建 Nic 交换机](static-creation-of-a-nic-switch.md)。

2.  如果 PF 微型端口驱动程序支持动态创建和配置 NIC 交换机，则它必须释放与指定的 NIC 交换机关联的硬件和软件资源。

    有关动态 NIC 交换机创建的详细信息，请参阅 [动态创建 Nic 交换机](dynamic-creation-of-a-nic-switch.md)。

3.  如果 PF 微型端口驱动程序支持动态创建 NIC 交换机，并在网络适配器上删除了所有 NIC 交换机，则驱动程序必须通过调用 [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization)禁用适配器上的虚拟化。 若要禁用虚拟化，网络适配器必须将 *EnableVirtualization* 参数设置为 FALSE，将 *NumVFs* 参数设置为零。

    [**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 清除 **NumVFs** 成员，并且 VF 在网络适配器的 PF 的 PCIe 配置空间中的 sr-iov 扩展功能结构中 **启用** 位。

    **注意**   如果 PF 微型端口驱动程序支持静态创建和配置 NIC 交换机，则在调用[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)时，它必须仅调用[**NdisMEnableVirtualization**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismenablevirtualization) 。

     

 

