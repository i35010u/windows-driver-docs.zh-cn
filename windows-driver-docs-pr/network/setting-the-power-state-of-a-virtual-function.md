---
title: 设置虚拟功能的电源状态
description: 设置虚拟功能的电源状态
ms.assetid: 7504677D-9B3A-47A2-9990-7BBF50A832EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 638eaa417f3071171511f719491b4f21abcdbe4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362027"
---
# <a name="setting-the-power-state-of-a-virtual-function"></a>设置虚拟功能的电源状态


基础驱动程序发出的一个对象标识符 (OID) 组请求[OID\_SRIOV\_设置\_VF\_POWER\_状态](https://msdn.microsoft.com/library/windows/hardware/hh451896)若要更改指定 PCI 的电源状态Express (PCIe) 虚拟函数 (VF) 上的网络适配器。 更改电源状态是一项特权的操作，因为基础驱动程序微型端口驱动程序的 PCIe 物理函数 (PF) 网络适配器上发出此 OID 集请求。 PF 微型端口驱动程序然后 VF 上设置指定的电源状态。

例如，虚拟化堆栈管理附加到 VF HYPER-V 子分区的电源状态。 堆栈将电源状态更改通过发出[OID\_SRIOV\_设置\_VF\_POWER\_状态](https://msdn.microsoft.com/library/windows/hardware/hh451896)到 PF 微型端口驱动程序。

它会发出 OID 集请求的前[OID\_SRIOV\_设置\_VF\_POWER\_状态](https://msdn.microsoft.com/library/windows/hardware/hh451896)，基础驱动程序必须设置的成员[ **NDIS\_SRIOV\_设置\_VF\_POWER\_状态\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451683)结构如下所示：

-   **VFId**成员必须设置为 VF 是要读取信息的标识符。

-   **PowerState**成员必须设置为取景器应转换为的电源状态。

-   如果网络适配器必须具有其唤醒\#（在 PCI Express 总线） 的信号或 PME\#信号 （在 PCI 总线） 添加进入低功耗状态，如**WakeEnable**成员必须设置为 TRUE。 否则，此成员必须设置为 FALSE。

当此 OID 集请求发出 PF 微型端口驱动程序，则它必须遵循以下准则：

-   PF 微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_设置\_VF\_POWER\_状态\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451683)结构，具有先前已分配的资源。 PF 微型端口驱动程序 OID 方法请求的过程将资源分配的 VF [OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。 如果指定的 VF 不处于已分配状态，该驱动程序必须故障 OID 请求。

-   电源状态操作只会影响指定的 VF。 该操作必须不影响其他 VFs 或同一个网络适配器上的 PF。

 

 





