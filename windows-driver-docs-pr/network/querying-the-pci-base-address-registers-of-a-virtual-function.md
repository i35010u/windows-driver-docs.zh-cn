---
title: 查询虚拟功能的 PCI 基址寄存器
description: 查询虚拟功能的 PCI 基址寄存器
ms.assetid: 99C2BF61-E87E-4C3B-BE7E-C16B5318EC1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee82180401a4dbcd3f01fb2e529eeb7440d7b0bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844870"
---
# <a name="querying-the-pci-base-address-registers-of-a-virtual-function"></a>查询虚拟功能的 PCI 基址寄存器

**注意**此方法只能由 Hyper-v 父分区的管理操作系统中运行的过量驱动程序使用。

PCI 总线驱动程序在 Hyper-v 父分区的管理操作系统中运行，它查询网络适配器的每个 PCI 基址寄存器（BAR）的内存或 i/o 地址空间要求。 PCI 总线驱动程序在第一次检测总线上的适配器时执行此查询。

通过此 PCI BAR 查询，PCI 总线驱动程序将确定以下各项：

-   网络适配器是否支持 PCI BAR。

-   如果支持一个条，则条需要多少内存或 i/o 地址空间。

PCI 驱动程序通过以下方式执行此 PCI BAR 查询：

1.  PCI 驱动程序首先将所有数据写入一个条形。

2.  然后，PCI 驱动程序会读取条来确定所需的内存或地址空间。 如果值为零，则表示网络适配器不支持此栏。

虚拟 PCI （VPCI）总线驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 当 PCI Express （PCIe）虚拟功能（VF）附加到子分区时，VPCI 总线驱动程序将公开用于 VF （*vf 网络适配器*）的虚拟网络适配器。 在执行此之前，VPCI bus 驱动程序必须执行 PCI BAR 查询来确定 VF 网络适配器所需的内存或地址空间。

由于对 PCI 配置空间的访问是一项特权操作，因此它只能由 Hyper-v 父分区的管理操作系统中运行的组件执行。 当 VPCI 总线驱动程序查询 PCI 条时，NDIS 发出[OID\_SRIOV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-probed-bars)的对象标识符（oid）查询请求，\_探测到 PF 微型端口驱动程序\_条。 此 OID 查询请求返回的结果将转发到 VPCI 总线驱动程序，以便它可以确定 VF 网络适配器所需的内存地址空间量。

**请注意**，  OID\_SRIOV\_BAR\_资源只能由 NDIS 发出。 OID 请求不得由过量驱动程序发出，如协议或筛选器驱动程序。

 

\_探测的 OID\_SRIOV 探测的\_条查询请求包含\_INFO 结构\_探测到的[**NDIS\_SRIOV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_probed_bars_info) 。 当 PF 微型端口驱动程序处理此 OID 时，驱动程序必须在由 NDIS\_SRIOV 的**BaseRegisterValuesOffset**成员引用的数组中返回 PCI BAR 值， **\_探测的\_条\_信息**结构。 对于数组中的每个偏移量，PF 微型端口驱动程序必须将数组元素设置为位于物理网络适配器 PCI 配置空间内相同偏移量的条的 ULONG 值。

驱动程序返回的每个条形值的值都必须与在管理操作系统中运行的 PCI 驱动程序执行的 PCI BAR 查询遵循的值相同。 PF 微型端口驱动程序可以调用[**NdisMQueryProbedBars**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismqueryprobedbars)来确定此信息。

有关 PCI 设备的基本地址寄存器的详细信息，请参阅*Pci 本地总线规范*。

 

 





