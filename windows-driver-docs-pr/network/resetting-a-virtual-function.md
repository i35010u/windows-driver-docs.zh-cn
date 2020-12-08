---
title: 重置虚拟功能
description: 重置虚拟功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95197bd8a8819b2e68226eadc593a2aec88153b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839991"
---
# <a name="resetting-a-virtual-function"></a>重置虚拟功能


过量驱动程序发出 (OID 的对象标识符) 设置 [oid \_ SRIOV \_ reset \_ vf](./oid-sriov-reset-vf.md) 的请求，以重置指定的 PCI Express (PCIE) 虚函数 (VF) 。 VF 是支持单根 i/o 虚拟化的网络适配器的硬件组件。 过量驱动程序将此 OID 集请求颁发给 PCI Express (PCIe 的微型端口驱动程序) 物理功能 (PF) 。

例如，虚拟化堆栈在 Hyper-v 父分区的管理操作系统中运行。 在堆栈从 Hyper-v 子分区分离 VF 之前，它会请求在 VF 上 (FLR) 的函数级别重置。 由于 FLR 是一项特权操作，因此只能由也在管理操作系统中运行的 PF 微型端口驱动程序执行。 若要请求指定的 VF 的 FLR，虚拟化堆栈会将 [OID \_ SRIOV \_ 重置 \_ VF](./oid-sriov-reset-vf.md)请求颁发给 PF 微型端口驱动程序。

在发出此 OID 集请求之前，过量驱动程序必须初始化 [**NDIS \_ SRIOV \_ RESET \_ VF \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters) 结构。 驱动程序必须将 **VFId** 成员设置为要重置的 VF 的标识符。

当它处理此 OID 请求时，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 [**NDIS \_ SRIOV \_ 重置 \_ Vf \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_reset_vf_parameters)结构的 **VFId** 成员指定的 VF 是否包含之前已分配的资源。 在 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)的 oid 方法请求期间，PF 微型端口驱动程序为 VF 分配资源。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   Reset 操作必须只影响指定的 VF。 此操作不能影响同一网络适配器上的其他 VFs 或 PF。

 

