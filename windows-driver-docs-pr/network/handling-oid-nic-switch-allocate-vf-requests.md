---
title: 处理 OID_NIC_SWITCH_ALLOCATE_VF 请求
description: 处理 OID_NIC_SWITCH_ALLOCATE_VF 请求
ms.assetid: B48A19D5-A768-4614-961D-1BD00762B6D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb57adb84e62e15812e16ee401e2e9d6d0a94558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842585"
---
# <a name="handling-oid_nic_switch_allocate_vf-requests"></a>处理 OID\_NIC\_交换机\_分配\_VF 请求


如果网络适配器上 PCI Express （PCIe）物理函数（PF）的微型端口驱动程序处理 OID\_\_NIC 的对象标识符（OID）方法请求[\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)，则会执行以下操作：

-   PF 微型端口驱动程序为网络适配器上的 PCIe 虚拟功能（VF）分配软件资源。 这些资源基于[**NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构中指定的参数进行配置。

-   PF 微型端口驱动程序将 VF 分配给网络适配器上的 NIC 交换机。 NIC 交换机由 NDIS\_NIC 的**SwitchId**成员确定[ **\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

    有关 NIC 交换机的详细信息，请参阅[Nic 交换机](nic-switches.md)。

-   PF 微型端口驱动程序使用 VF 标识符更新**VFId**成员。 此标识符是从零开始的索引，并且在通过 PF 微型端口驱动程序在 NIC 交换机上分配的所有 VFs 中必须是唯一的。

    占用空间的驱动程序使用 Oid 的连续 OID 请求中的**VFId**成员的值[\_nic\_switch\_FREE\_vf](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)或 OID\_nic\_\_[VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)。

-   PF 微型端口驱动程序使用用于 VF 的 PCIe 请求者标识符（RID）更新**RequestorId**成员。

    微型端口驱动程序调用[**NdisMGetVirtualFunctionLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionlocation) ，以获取与 VF 对应的 RID 信息。 然后，该驱动程序使用 NDIS 创建 RID，\_基于对**NdisMGetVirtualFunctionLocation**的调用返回的信息[**生成\_RID**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-make-rid)宏。

    虚拟化堆栈使用 RID 来重新映射 PF 和 VF 之间的 DMA 和中断。 RID 还允许硬件输入/输出内存管理单元（IOMMU）将来宾物理地址转换为主机物理地址。

-   PF 微型端口驱动程序初始化并公开 VF。 这会使 VF 可供虚拟化堆栈使用。

如果 PF 微型端口驱动程序可以成功分配必要的软件资源并初始化 VF，则驱动程序将完成 OID 请求，并将 NDIS\_状态\_成功。 PF 微型端口驱动程序必须保留每个分配的 VF 的 VF Id。 NDIS 和过量驱动程序使用对 PF 微型端口驱动程序的后续 OID 请求中的 VF 标识符来执行各种操作，如重置或释放 VF。

**请注意**  分配 vf 的资源时，vf 处于未连接状态，因为虚拟端口（VPort）未附加到 VF。 过量驱动程序可以发出 oid\_NIC 的 OID 请求[\_交换机\_create\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)创建 VPORT 并将其附加到 VF。 有关详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

 

 

 





