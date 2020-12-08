---
title: 设置虚拟功能的电源状态
description: 设置虚拟功能的电源状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a0864bf4f8fb74f1e718957840269a15f97ddf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820005"
---
# <a name="setting-the-power-state-of-a-virtual-function"></a>设置虚拟功能的电源状态


过量驱动程序发出 (OID 的对象标识符) 设置 Oid 的请求，以更改网络适配器上指定 PCI Express (PCIe) 虚函数 (VF 的电源状态 [ \_ \_ \_ \_ \_ ](./oid-sriov-set-vf-power-state.md) 。 由于更改电源状态是特权操作，因此过量驱动程序会在网络适配器上向 PCIe 物理功能 (PF) 的微型端口驱动程序发出此 OID 设置请求。 然后，PF 微型端口驱动程序将设置 VF 上指定的电源状态。

例如，虚拟化堆栈管理附加到 VF 的 Hyper-v 子分区的电源状态。 堆栈通过发出 OID SRIOV，并将 [ \_ \_ \_ VF \_ 电源 \_ 状态设置](./oid-sriov-set-vf-power-state.md) 为 PF 微型端口驱动程序来更改电源状态。

在发出 oid [ \_ SRIOV \_ set \_ VF \_ 电源 \_ 状态](./oid-sriov-set-vf-power-state.md)的 oid 集请求之前，过量驱动程序必须按以下方式设置 [**NDIS \_ SRIOV \_ 设置 \_ vf \_ 电源 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters) 结构的成员：

-   **VFId** 成员必须设置为要从中读取信息的 VF 的标识符。

-   **PowerState** 成员必须设置为 VF 应转换到的电源状态。

-   如果网络适配器必须 \# 在 Pci Express 总线) 上 (其唤醒信号 \# ，并且 pci 总线上的 PME 信号 () 在其进入低功耗状态时被断言，则必须将 **WakeEnable** 成员设置为 TRUE。 否则，此成员必须设置为 FALSE。

当向此 OID 集请求颁发了 PF 微型端口驱动程序时，必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 [**NDIS \_ SRIOV \_ SET \_ vf \_ 电源 \_ 状态 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_set_vf_power_state_parameters)结构的 **VFId** 成员指定的 VF 是否具有以前分配的资源。 在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)的 oid 方法请求期间，PF 微型端口驱动程序为 VF 分配资源。 如果指定的 VF 未处于已分配状态，则驱动程序必须使 OID 请求失败。

-   电源状态操作只能影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

 

