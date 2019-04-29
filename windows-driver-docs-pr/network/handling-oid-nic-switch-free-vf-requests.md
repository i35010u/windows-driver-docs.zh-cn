---
title: 处理 OID_NIC_SWITCH_FREE_VF 请求
description: 处理 OID_NIC_SWITCH_FREE_VF 请求
ms.assetid: 56134421-6D3C-4A40-B7EE-FDB729D46DEB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014b2843f9004fe81a1a56200cd3e1f0c52e2692
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349713"
---
# <a name="handling-oidnicswitchfreevf-requests"></a>处理 OID\_NIC\_交换机\_免费\_VF 请求


当微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 网络适配器上处理的对象标识符 (OID) 的集请求[OID\_NIC\_交换机\_免费\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)，它执行以下操作：

-   **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构 OID 请求包含一个指向[ **NDIS\_NIC\_交换机\_免费\_VF\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451579)结构。 PF 微型端口驱动程序必须验证的 PCIe 虚拟函数 (VF)，由指定的标识符**VFId**成员，是否有效。 如果不为 true，该驱动程序必须通过返回 NDIS 故障 OID 集请求\_状态\_无效\_参数。

-   PF 微型端口驱动程序必须验证 VF 的资源具有以前分配的 OID 方法请求通过[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。 如果不为 true，该驱动程序必须通过返回 NDIS 故障 OID 集请求\_状态\_无效\_参数。

-   PF 微型端口驱动程序必须验证任何虚拟端口 (VPorts) 当前附加到 VF。 如果不为 true，该驱动程序必须通过返回 NDIS 失败集请求\_状态\_无效\_参数。

-   PF 微型端口驱动程序必须释放所有已分配给指定 VF 的软件资源。

-   PF 微型端口驱动程序必须分离的网络适配器上的 NIC 开关从 VF。

如果成功，PF 微型端口驱动程序可以释放已分配的软件资源并分离 NIC 交换机 VF，驱动程序完成 OID 请求使用 NDIS\_状态\_成功。

**请注意**  NDIS 可保证所有微型端口上分配 VFs NDIS 颁发的 OID 集请求之前释放[OID\_NIC\_开关\_删除\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451817)到 PF 微型端口驱动程序。 当它处理此 OID 时，该驱动程序中删除网络适配器上的 NIC 交换机。

 

 

 





