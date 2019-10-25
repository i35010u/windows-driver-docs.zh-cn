---
title: 重置虚拟功能
description: 重置虚拟功能
ms.assetid: 4B7A4E02-6383-45FB-9F75-D17C047C40D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1ec9e3385fb7b39720bbea442f0f67fbdc547dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842026"
---
# <a name="resetting-a-virtual-function"></a>重置虚拟功能


过量驱动程序发出 OID\_SRIOV 的对象标识符（OID）设置请求[\_reset\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)来重置指定的 PCI Express （PCIe）虚拟功能（VF）。 VF 是支持单根 i/o 虚拟化的网络适配器的硬件组件。 过量驱动程序将此 OID 集请求颁发给 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序。

例如，虚拟化堆栈在 Hyper-v 父分区的管理操作系统中运行。 在堆栈从 Hyper-v 子分区分离 VF 之前，它会在 VF 上请求函数级别重置（FLR）。 由于 FLR 是一项特权操作，因此只能由也在管理操作系统中运行的 PF 微型端口驱动程序执行。 若要请求指定的 VF 的 FLR，虚拟化堆栈会发出[OID\_SRIOV\_RESET\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-reset-vf)请求发送到 PF 微型端口驱动程序。

在发出此 OID 集请求之前，过量驱动程序必须初始化[**NDIS\_SRIOV\_RESET\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构。 驱动程序必须将**VFId**成员设置为要重置的 VF 的标识符。

当它处理此 OID 请求时，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 NDIS\_SRIOV 的**VFId**成员指定的 vf 是否[ **\_RESET\_vf\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构）是否具有以前分配的资源。 在 oid 的 OID 方法请求中，PF 微型端口驱动程序为一个 VF 分配资源[\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   Reset 操作必须只影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

 

 





