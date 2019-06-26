---
title: 重置虚拟功能
description: 重置虚拟功能
ms.assetid: 4B7A4E02-6383-45FB-9F75-D17C047C40D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62bc2c3c71f04fa068330668348fe231f3afd775
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384710"
---
# <a name="resetting-a-virtual-function"></a>重置虚拟功能


基础驱动程序发出的一个对象标识符 (OID) 组请求[OID\_SRIOV\_重置\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)重置指定 PCI Express (PCIe) 虚拟函数 (VF)。 VF 是支持单根 I/O 虚拟化的网络适配器的硬件组件。 基础驱动程序微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 向颁发此 OID 集请求。

例如，虚拟化堆栈在 HYPER-V 父分区的管理操作系统中运行。 在堆栈中分离 VF 从 HYPER-V 子分区之前，它将请求函数级别重置 (FLR) vf。 由于 FLR 是一项特权的操作，它可以执行只能由管理操作系统中还运行 PF 微型端口驱动程序。 若要请求指定 VF，虚拟化堆栈问题 FLR [OID\_SRIOV\_重置\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)PF 微型端口驱动程序的请求。

它会发出此 OID 集请求之前，必须初始化基础驱动程序[ **NDIS\_SRIOV\_重置\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构。 该驱动程序必须设置**VFId** VF 要重置的标识符的成员。

当它处理此 OID 请求时，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_重置\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构，具有先前已分配的资源。 PF 微型端口驱动程序 OID 方法请求的过程将资源分配的 VF [OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

-   重置操作只会影响指定的 VF。 该操作必须不影响其他 VFs 或同一个网络适配器上的 PF。

 

 





