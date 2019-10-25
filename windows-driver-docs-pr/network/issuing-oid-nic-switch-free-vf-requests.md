---
title: 发出 OID_NIC_SWITCH_FREE_VF 请求
description: 发出 OID_NIC_SWITCH_FREE_VF 请求
ms.assetid: D9A8548C-02D8-4537-9053-6B262004CBC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06eb856d509f1d09b3b63cf1982e86840e476143
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844152"
---
# <a name="issuing-oid_nic_switch_free_vf-requests"></a>颁发 OID\_NIC\_交换机\_免费\_VF 请求


过量驱动程序会发出 Oid\_NIC 的对象标识符（OID）设置请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 PCI Express （PCIe）虚拟功能（VF）的资源。 之前已通过 oid 的 OID 方法请求对这些资源进行了分配[\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

过量驱动程序发出[OID\_NIC\_交换机\_FREE\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)将请求设置为 PCIe 物理功能（PF）的微型端口驱动程序。 在发出此 OID 请求之前，过量驱动程序必须执行以下操作：

1.  过量驱动程序必须确保 VF 未连接到网络适配器的 NIC 交换机上的任何虚拟端口（VPort）。 过量驱动程序必须发出 oid\_NIC 的 OID 设置请求[\_交换机\_delete\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-vport)删除附加到 VF 的所有 VPorts。 有关详细信息，请参阅[删除虚拟端口](deleting-a-virtual-port.md)。

2.  过量驱动程序将[**NDIS\_NIC\_交换机\_FREE\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构。 驱动程序必须将**VFId**成员设置为在 OID\_NIC 的 oid 方法请求中返回的 VF 标识符[\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

过量驱动程序会按照以下步骤发出 Oid\_NIC 的 OID 集请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf) ：

1.  上层驱动程序为 OID 方法请求初始化[**NDIS\_oid\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构。 驱动程序将**InformationBuffer**成员设置为指向已初始化[**NDIS\_NIC 的指针\_交换机\_免费\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构。

2.  过量驱动程序调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)将 OID 请求颁发给基础 PF 微型端口驱动程序。

在过量驱动程序为 VF 请求分配资源后，该驱动程序是唯一可请求为同一 VF 释放资源的组件。 过量驱动程序必须发出 oid\_NIC 的 OID 集请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 VF 资源。 在可以停止过量驱动程序之前，它必须释放由驱动程序的 OID\_NIC 分配的每个 VF 的资源[\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)请求。

**请注意**   如果过量驱动程序\_NIC 发出 oid 方法请求[NIC\_开关\_分配\_vf](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)为 VF 分配资源，则该驱动程序是可以请求释放相同 VF 的资源。 过量驱动程序必须发出 oid\_NIC 的 OID 集请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)来释放 VF 资源。 在可以停止过量驱动程序之前，它必须释放由驱动程序的 OID\_NIC 分配的每个 VF 的资源\_交换机\_分配\_VF 请求。

 

 

 





