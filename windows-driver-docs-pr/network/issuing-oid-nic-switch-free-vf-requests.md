---
title: 发出 OID_NIC_SWITCH_FREE_VF 请求
description: 发出 OID_NIC_SWITCH_FREE_VF 请求
ms.assetid: D9A8548C-02D8-4537-9053-6B262004CBC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99e2ad89b0fd119ec7290a98caeaa9aca65537c0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215614"
---
# <a name="issuing-oid_nic_switch_free_vf-requests"></a>发出 OID \_ NIC \_ 交换机 \_ 免费 \_ VF 请求


过量驱动程序会 (OID 发出对象标识符) 设置 [oid \_ NIC 交换机的 \_ 请求 \_ 自由 \_ VF](./oid-nic-switch-free-vf.md) ，以释放 PCI Express (PCIe) 虚函数 (VF) 的资源。 以前通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 oid 方法请求分配了这些资源。

过量驱动程序向 PCIe 物理功能 (PF) 的微型端口驱动程序的 " [OID \_ NIC \_ 开关 \_ 免费 \_ VF](./oid-nic-switch-free-vf.md) 集" 请求发出 OID。 在发出此 OID 请求之前，过量驱动程序必须执行以下操作：

1.  过量驱动程序必须确保 VF 未连接到网络适配器的 NIC 交换机上 (VPort) 的任何虚拟端口。 过量驱动程序必须发出 oid [ \_ NIC \_ SWITCH \_ delete \_ VPORT](./oid-nic-switch-delete-vport.md) 的 oid 设置请求，才能删除附加到 VF 的所有 VPorts。 有关详细信息，请参阅 [删除虚拟端口](deleting-a-virtual-port.md)。

2.  过量驱动程序初始化 [**NDIS \_ NIC \_ 交换机 \_ 自由 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters) 结构。 驱动程序必须将 **VFId** 成员设置为在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)的 oid 方法请求中返回的 VF 标识符。

过量驱动程序通过执行以下步骤发出 [oid \_ NIC \_ 交换机 \_ 自由 \_ VF](./oid-nic-switch-free-vf.md) 的 oid 设置请求：

1.  上层驱动程序为 OID 方法请求初始化 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构。 驱动程序将 **InformationBuffer** 成员设置为指向已初始化的 [**NDIS \_ NIC \_ 交换机 \_ 自由 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters) 结构的指针。

2.  过量驱动程序调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 将 OID 请求颁发给基础 PF 微型端口驱动程序。

在过量驱动程序为 VF 请求分配资源后，该驱动程序是唯一可请求为同一 VF 释放资源的组件。 过量驱动程序必须发出 oid [ \_ NIC \_ 交换机 \_ 自由 \_ vf](./oid-nic-switch-free-vf.md) 的 OID 设置请求，以释放 vf 资源。 在停止过量驱动程序之前，必须释放由驱动程序的 [OID \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md) 请求分配的每个 VF 的资源。

**注意**   如果过量驱动程序发出 Oid NIC 交换机的 OID 方法请求，则[ \_ \_ \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)来分配用于 vf 的资源，该驱动程序是可以请求为同一 vf 释放资源的唯一组件。 过量驱动程序必须发出 oid [ \_ NIC \_ 交换机 \_ 自由 \_ vf](./oid-nic-switch-free-vf.md) 的 OID 设置请求，以释放 vf 资源。 在停止过量驱动程序之前，必须释放由驱动程序的 OID \_ NIC \_ 交换机 \_ 分配 \_ vf 请求分配的每个 VF 的资源。

 

 

