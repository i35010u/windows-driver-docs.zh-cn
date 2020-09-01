---
title: 处理 OID_NIC_SWITCH_FREE_VF 请求
description: 处理 OID_NIC_SWITCH_FREE_VF 请求
ms.assetid: 56134421-6D3C-4A40-B7EE-FDB729D46DEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00fad7e066a50439dc7ac0f2be2f501a7e7c57b1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218410"
---
# <a name="handling-oid_nic_switch_free_vf-requests"></a>处理 OID \_ NIC \_ 交换机 \_ 免费 \_ VF 请求


当网络适配器上的 PCI Express (PCIe) 物理功能 (PF) 的微型端口驱动程序处理对象标识符 (OID) 设置 [oid \_ NIC \_ 交换机 \_ 自由 \_ VF](./oid-nic-switch-free-vf.md)的请求时，它执行以下操作：

-   OID 请求的[**ndis \_ oid \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ NIC \_ 交换机 \_ 自由 \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构的指针。 PF 微型端口驱动程序必须验证 (VF) （由 **VFId** 成员指定）的 PCIe 虚拟函数的标识符是否有效。 如果不是这样，则驱动程序必须通过返回 NDIS \_ STATUS 无效参数来使 OID 设置请求失败 \_ \_ 。

-   PF 微型端口驱动程序必须验证是否已通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 oid 方法请求为 VF 分配资源。 如果不是这样，则驱动程序必须通过返回 NDIS \_ STATUS 无效参数来使 OID 设置请求失败 \_ \_ 。

-   PF 微型端口驱动程序必须验证当前是否没有 (VPorts) 的虚拟端口连接到 VF。 如果不是这样，则驱动程序必须通过返回 NDIS \_ STATUS 无效参数来使设置请求失败 \_ \_ 。

-   PF 微型端口驱动程序必须释放为指定的 VF 分配的所有软件资源。

-   PF 微型端口驱动程序必须将 VF 从网络适配器上的 NIC 交换机中分离出来。

如果 PF 微型端口驱动程序可以成功释放已分配的软件资源，并将 VF 与 NIC 交换机分离，则驱动程序将完成 OID 请求，并提供 NDIS \_ 状态 \_ 成功。

**注意**   NDIS 保证在 NDIS 发出 oid [ \_ NIC \_ 交换机 \_ 删除 \_ 交换机](./oid-nic-switch-delete-switch.md)到 PF 微型端口驱动程序的 oid 集请求之前，释放在微型端口上分配的所有 VFs。 当它处理此 OID 时，驱动程序将删除网络适配器上的 NIC 交换机。

 

 

