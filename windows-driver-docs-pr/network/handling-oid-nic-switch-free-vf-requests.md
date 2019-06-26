---
title: 处理 OID_NIC_SWITCH_FREE_VF 请求
description: 处理 OID_NIC_SWITCH_FREE_VF 请求
ms.assetid: 56134421-6D3C-4A40-B7EE-FDB729D46DEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e919e539b363a2737ce31391f77c6415cead1c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379793"
---
# <a name="handling-oidnicswitchfreevf-requests"></a>处理 OID\_NIC\_交换机\_免费\_VF 请求


当微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 网络适配器上处理的对象标识符 (OID) 的集请求[OID\_NIC\_交换机\_免费\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-free-vf)，它执行以下操作：

-   **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构 OID 请求包含一个指向[ **NDIS\_NIC\_交换机\_免费\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_free_vf_parameters)结构。 PF 微型端口驱动程序必须验证的 PCIe 虚拟函数 (VF)，由指定的标识符**VFId**成员，是否有效。 如果不为 true，该驱动程序必须通过返回 NDIS 故障 OID 集请求\_状态\_无效\_参数。

-   PF 微型端口驱动程序必须验证 VF 的资源具有以前分配的 OID 方法请求通过[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果不为 true，该驱动程序必须通过返回 NDIS 故障 OID 集请求\_状态\_无效\_参数。

-   PF 微型端口驱动程序必须验证任何虚拟端口 (VPorts) 当前附加到 VF。 如果不为 true，该驱动程序必须通过返回 NDIS 失败集请求\_状态\_无效\_参数。

-   PF 微型端口驱动程序必须释放所有已分配给指定 VF 的软件资源。

-   PF 微型端口驱动程序必须分离的网络适配器上的 NIC 开关从 VF。

如果成功，PF 微型端口驱动程序可以释放已分配的软件资源并分离 NIC 交换机 VF，驱动程序完成 OID 请求使用 NDIS\_状态\_成功。

**请注意**  NDIS 可保证所有微型端口上分配 VFs NDIS 颁发的 OID 集请求之前释放[OID\_NIC\_开关\_删除\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-delete-switch)到 PF 微型端口驱动程序。 当它处理此 OID 时，该驱动程序中删除网络适配器上的 NIC 交换机。

 

 

 





