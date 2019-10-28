---
title: 枚举网络适配器上的虚拟功能
description: 枚举网络适配器上的虚拟功能
ms.assetid: 3AAF2D8B-9C7A-4E5B-86B6-264ACA5EA492
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9777cd2e1a00b5b556064e76cba3f96ccbccb5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838114"
---
# <a name="enumerating-virtual-functions-on-a-network-adapter"></a>枚举网络适配器上的虚拟功能


过量驱动程序或用户应用程序可以在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上获取所有 PCI Express （PCIe）虚拟功能（VFs）的列表。 驱动程序或应用程序发出 OID\_NIC 的对象标识符（OID）方法请求[\_交换机\_枚举\_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)获取此列表。

在驱动程序或应用程序发出 OID 请求之前，它必须将[**NDIS\_NIC\_交换机\_\_VF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)与请求一起传递\_数组结构。 在初始化 NDIS\_NIC 时，驱动程序或应用程序必须遵循以下准则 **\_交换机\_VF\_信息\_数组**结构：

-   如果 NDIS\_NIC\_交换机\_VF\_信息\_数组\_在**Flags**成员中设置\_特定\_交换机标志，过量驱动程序或应用程序必须将**SwitchId**成员设置为 sr-iov 网络适配器上的 NIC 交换机的标识符。 通过以这种方式设置这些成员，只会为 SR-IOV 网络适配器上指定的 NIC 交换机返回 VF 信息。

    **注意** 过量驱动程序和用户模式应用程序可以通过[\_交换机\_枚举\_开关发出 oid\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)的 oid 查询请求，从而获取 nic 交换机标识符。

-   如果**Flags**成员设置为零，则驱动程序或应用程序必须将**SwitchId**成员设置为零。 通过以这种方式设置这些成员，将为 SR-IOV 网络适配器上的所有 NIC 交换机返回 VF 信息。

    **注意** 从 Windows Server 2012 开始，Windows 只支持网络适配器上的默认 NIC 交换机。 不管**flags**成员中的标志集如何，都必须将**SwitchId**成员设置为 NDIS\_默认\_交换机\_ID。

成功从此 OID 查询请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   [**NDIS\_NIC\_交换机\_VF\_信息\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)定义数组中元素数目的数组结构。

-   [**NDIS\_NIC 的数组\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构。 其中每个结构都包含有关网络适配器的 NIC 交换机上单个 VF 的信息。 VF 通过 oid\_NIC 的 OID 方法请求（ [\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)）附加到 nic 开关。

    **注意** 如果网络适配器上没有连接到任何一个 NIC 交换机的 VFs，NDIS\_NIC 的**NumElements**成员将[ **\_交换机\_VF\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)结构设置为零，且没有任何[**NDIS\_NIC\_交换机返回\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构。

    有关 NIC 交换机的详细信息，请参阅[Nic 交换机](nic-switches.md)。

NDIS 为微型端口驱动程序[\_枚举\_VFS 请求处理 OID\_NIC\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   Oid [\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)的 oid 方法请求。

-   OID\_NIC 上设置 Oid 的请求[\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)。