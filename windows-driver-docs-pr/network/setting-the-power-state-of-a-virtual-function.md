---
title: 设置虚拟功能的电源状态
description: 设置虚拟功能的电源状态
ms.assetid: 7504677D-9B3A-47A2-9990-7BBF50A832EA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7846d99bf5b4fa47ba03bb56b3d3c9be10fcd07
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841925"
---
# <a name="setting-the-power-state-of-a-virtual-function"></a>设置虚拟功能的电源状态


过量驱动程序发出 OID\_的对象标识符（OID）设置请求[\_设置\_VF\_POWER\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)，以更改网络适配器上指定 PCI Express （PCIe）虚拟功能（VF）的电源状态。 由于更改电源状态是特权操作，因此过量驱动程序将此 OID 集请求颁发给网络适配器上 PCIe 物理功能（PF）的微型端口驱动程序。 然后，PF 微型端口驱动程序将设置 VF 上指定的电源状态。

例如，虚拟化堆栈管理附加到 VF 的 Hyper-v 子分区的电源状态。 堆栈通过发出 OID 来更改电源状态， [\_SRIOV\_将\_VF\_power\_状态设置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)为 PF 微型端口驱动程序。

在发出 oid\_SRIOV 的 OID 集请求之前[\_将\_VF\_POWER\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-set-vf-power-state)，而过量驱动程序必须将[**NDIS\_SRIOV 的成员设置\_\_\_\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)结构，如下所示：

-   **VFId**成员必须设置为要从中读取信息的 VF 的标识符。

-   **PowerState**成员必须设置为 VF 应转换到的电源状态。

-   如果网络适配器必须具有其唤醒\# 信号（在 PCI Express 总线上）或 PME\# 信号（在 PCI 总线上）在进入低功耗状态时断言，则必须将**WakeEnable**成员设置为 TRUE。 否则，此成员必须设置为 FALSE。

当向此 OID 集请求颁发了 PF 微型端口驱动程序时，必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 NDIS\_SRIOV 的**VFId**成员指定的 VF [ **\_设置\_VF\_POWER\_状态\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)结构，具有以前的资源分配. 在 oid 的 OID 方法请求中，PF 微型端口驱动程序为一个 VF 分配资源[\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果指定的 VF 未处于已分配状态，则驱动程序必须使 OID 请求失败。

-   电源状态操作只能影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

 

 





