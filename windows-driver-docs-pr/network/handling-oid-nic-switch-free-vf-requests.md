---
title: 处理 OID_NIC_SWITCH_FREE_VF 请求
description: 处理 OID_NIC_SWITCH_FREE_VF 请求
ms.assetid: 56134421-6D3C-4A40-B7EE-FDB729D46DEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da425eed0725953e4078ce0775d472ef9e0fc296
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842581"
---
# <a name="handling-oid_nic_switch_free_vf-requests"></a>处理 OID\_NIC\_交换机\_免费\_VF 请求


如果网络适配器上 PCI Express （PCIe）物理函数（PF）的微型端口驱动程序处理 OID\_NIC 的对象标识符（OID）设置请求[\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)，则执行以下操作：

-   \_oid 的[**ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_NIC 的指针\_交换机\_免费\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构。 PF 微型端口驱动程序必须验证**VFId**成员指定的 PCIe 虚拟函数（VF）的标识符是否有效。 如果不是这种情况，则驱动程序必须通过返回 NDIS\_状态\_无效\_参数来使 OID 设置请求失败。

-   PF 微型端口驱动程序必须验证是否已通过 oid 的 oid 方法请求为 VF 分配了资源， [\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果不是这种情况，则驱动程序必须通过返回 NDIS\_状态\_无效\_参数来使 OID 设置请求失败。

-   PF 微型端口驱动程序必须验证当前没有任何虚拟端口（VPorts）附加到 VF。 如果不是这样，则驱动程序必须通过返回 NDIS\_状态\_无效\_参数来使设置请求失败。

-   PF 微型端口驱动程序必须释放为指定的 VF 分配的所有软件资源。

-   PF 微型端口驱动程序必须将 VF 从网络适配器上的 NIC 交换机中分离出来。

如果 PF 微型端口驱动程序可以成功释放已分配的软件资源并将 VF 与 NIC 交换机分离，则驱动程序将完成 OID 请求，并将 NDIS\_状态\_SUCCESS。

**请注意**  ndis 可保证在 ndis 发出 OID 的 oid 集请求之前释放在微型端口上分配的所有 VFS [\_NIC\_switch\_删除\_切换](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)到 PF 微型端口驱动程序。 当它处理此 OID 时，驱动程序将删除网络适配器上的 NIC 交换机。

 

 

 





