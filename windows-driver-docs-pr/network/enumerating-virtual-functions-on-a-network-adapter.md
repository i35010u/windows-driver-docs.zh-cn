---
title: 枚举网络适配器上的虚拟功能
description: 枚举网络适配器上的虚拟功能
ms.assetid: 3AAF2D8B-9C7A-4E5B-86B6-264ACA5EA492
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b4269b6db9b12c828fb6a4ee9a2a5eefdc1ef94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354566"
---
# <a name="enumerating-virtual-functions-on-a-network-adapter"></a>枚举网络适配器上的虚拟功能


基础驱动程序或用户应用程序可以获取所有 PCI Express (PCIe) 虚函数 (VFs) 支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器上的列表。 驱动程序或应用程序发出的对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_枚举\_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)来获取此列表。

驱动程序或应用程序发出 OID 请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_VF\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)随请求一起传递的结构。 驱动程序或应用程序初始化时，必须遵循这些准则**NDIS\_NIC\_交换机\_VF\_信息\_数组**结构：

-   如果 NDIS\_NIC\_交换机\_VF\_信息\_数组\_枚举\_ON\_特定\_中设置了开关标志**标志**成员、 过量的驱动程序或应用程序必须设置**SwitchId**成员添加到 NIC 交换机的 SR-IOV 网络适配器上的标识符。 通过以这种方式设置这些成员，仅对指定的 NIC 的 SR-IOV 网络适配器上切换，则返回 VF 信息。

    **请注意**过量的驱动程序和用户模式应用程序可以通过发出的 OID 查询请求获取 NIC 交换机标识符[OID\_NIC\_切换\_枚举\_交换机](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches).

-   如果**标志**成员设置为零，则驱动程序或应用程序必须设置**SwitchId**为零的成员。 通过以这种方式设置这些成员，VF 返回信息的所有 NIC 开关 SR-IOV 网络适配器上。

    **请注意**从 Windows Server 2012 开始，Windows 上的网络适配器支持仅默认 NIC 切换。 无论中设置的标志**标志**成员**SwitchId**成员必须设置为 NDIS\_默认\_开关\_id。

通过此 OID 查询请求的成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向包含以下各项的缓冲区的指针：

-   [ **NDIS\_NIC\_交换机\_VF\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)结构，用于定义数组中元素数。

-   一个数组[ **NDIS\_NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构。 包含有关单个 VF NIC 交换机上的网络适配器的信息，以及每个这些结构。 取景器附加到通过 OID 方法请求的 NIC 交换机[OID\_NIC\_切换\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

    **请注意**如果没有 VFs 已附加到网络适配器上的 NIC 交换机**NumElements**的成员[ **NDIS\_NIC\_切换\_VF\_INFO\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)结构设置为零并且没有[ **NDIS\_NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)返回结构。

    有关 NIC 开关的详细信息，请参阅[NIC 开关](nic-switches.md)。

NDIS 句柄[OID\_NIC\_交换机\_枚举\_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)微型端口驱动程序的请求。 NDIS 从它所维护从检查以下源的数据的内部缓存中返回的信息：

-   OID 的方法请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

-   设置的请求通过 OID [OID\_NIC\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)。