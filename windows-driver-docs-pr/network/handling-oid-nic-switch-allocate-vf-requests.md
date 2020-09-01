---
title: 处理 OID_NIC_SWITCH_ALLOCATE_VF 请求
description: 处理 OID_NIC_SWITCH_ALLOCATE_VF 请求
ms.assetid: B48A19D5-A768-4614-961D-1BD00762B6D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88176f45cda3b06f2e576d9d8565bec554f0c05a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207295"
---
# <a name="handling-oid_nic_switch_allocate_vf-requests"></a>处理 OID \_ NIC \_ 交换机 \_ 分配 \_ VF 请求


当网络适配器上的 PCI Express (PCIe) 物理功能 () PF 的微型端口驱动程序处理对象标识符 (OID 时，Oid NIC 交换机的方法请求会 [ \_ \_ \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)，它执行以下操作：

-   PF 小型端口驱动程序为网络适配器上 (VF) 分配 PCIe 虚拟功能的软件资源。 这些资源基于 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters) 结构中指定的参数进行配置。

-   PF 微型端口驱动程序将 VF 分配给网络适配器上的 NIC 交换机。 NIC 交换机由[**NDIS \_ NIC \_ 交换机 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构的**SwitchId**成员标识。

    有关 NIC 交换机的详细信息，请参阅 [Nic 交换机](nic-switches.md)。

-   PF 微型端口驱动程序使用 VF 标识符更新 **VFId** 成员。 此标识符是从零开始的索引，并且在通过 PF 微型端口驱动程序在 NIC 交换机上分配的所有 VFs 中必须是唯一的。

    占用空间的驱动程序在[oid \_ nic \_ 开关 \_ 免费 \_ VF](./oid-nic-switch-free-vf.md)或[OID \_ nic \_ 交换机 \_ VF \_ 参数](./oid-nic-switch-vf-parameters.md)的后续 oid 请求中使用**VFId**成员的值。

-   PF 微型端口驱动程序使用 (RID) 为 VF 请求的 PCIe 请求程序标识符更新 **RequestorId** 成员。

    微型端口驱动程序调用 [**NdisMGetVirtualFunctionLocation**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionlocation) ，以获取与 VF 对应的 RID 信息。 然后，该驱动程序将根据调用**NdisMGetVirtualFunctionLocation**所返回的信息，使用[**NDIS \_ MAKE \_ rid**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_make_rid)宏创建 rid。

    虚拟化堆栈使用 RID 来重新映射 PF 和 VF 之间的 DMA 和中断。 RID 还允许硬件输入/输出内存管理单元 (IOMMU) 将来宾物理地址转换为主机物理地址。

-   PF 微型端口驱动程序初始化并公开 VF。 这会使 VF 可供虚拟化堆栈使用。

如果 PF 微型端口驱动程序可以成功分配所需的软件资源并初始化 VF，则驱动程序将完成 OID 请求，并获得 NDIS \_ 状态 \_ SUCCESS。 PF 微型端口驱动程序必须保留每个分配的 VF 的 VF Id。 NDIS 和过量驱动程序使用对 PF 微型端口驱动程序的后续 OID 请求中的 VF 标识符来执行各种操作，如重置或释放 VF。

**注意**   分配 VF 的资源后，VF 处于未连接状态，因为虚拟端口 (VPort) 未附加到 VF。 过量驱动程序可以发出 [oid \_ NIC \_ SWITCH \_ create \_ VPORT](./oid-nic-switch-create-vport.md) 的 oid 请求，以创建 VPORT 并将其附加到 VF。 有关详细信息，请参阅 [创建虚拟端口](creating-a-virtual-port.md)。

 

 

