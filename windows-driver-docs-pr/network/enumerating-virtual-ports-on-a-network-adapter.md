---
title: 枚举网络适配器上的虚拟端口
description: 枚举网络适配器上的虚拟端口
ms.assetid: 437C3356-4CC7-4128-9E61-FD01157F4FD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb889837882d83edc26e7b47fedc3b8e7ed9dd9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834768"
---
# <a name="enumerating-virtual-ports-on-a-network-adapter"></a>枚举网络适配器上的虚拟端口


过量驱动程序或用户应用程序可以在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器的 NIC 交换机上获取所有虚拟端口（VPorts）的列表。 驱动程序或应用程序发出 OID\_NIC 的对象标识符（OID）方法请求[\_交换机\_枚举\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)以获取此列表。

成功从此 OID 查询请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   [**NDIS\_NIC\_交换机\_VPORT\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)结构，该结构定义数组中的元素数目。

-   [**NDIS\_NIC 的数组\_交换机\_VPORT\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构。 其中每个结构都包含有关网络适配器的 NIC 交换机上的 VPort 的信息。

    **注意**  如果未在网络适配器上创建 VPorts，则驱动程序会将 NDIS\_\_NIC 的**NumElements**成员设置[ **\_VPORT\_info\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)结构设置为零，且不会返回[**ndis\_NIC\_交换机\_VPORT\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构。

     

在上层的驱动程序或用户应用程序[\_交换机\_枚举\_VPORTS 请求发出\_OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)之前，它必须初始化[**NDIS\_nic\_交换机\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)与请求一起传递\_\_的数组结构。 在初始化 NDIS\_NIC 时，驱动程序或应用程序必须遵循以下准则 **\_交换机\_VPORT\_信息\_数组**结构：

-   如果在**Flags**成员中设置\_特定\_交换机标志上的 NDIS\_NIC\_交换机\_VPORT\_信息\_数组\_枚举\_，则会为指定 NIC 交换机上创建的所有 VPorts 返回信息。 NIC 交换机由该结构的**SwitchId**成员指定。

    **注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为*默认 NIC 交换机*，由 NDIS\_默认\_交换机\_ID 标识符引用。 不管**flags**成员中设置了哪些标志，都必须将**SwitchId**成员设置为 NDIS\_默认\_交换机\_ID。

     

-   如果在**Flags**成员中设置\_特定\_函数标志上的 NDIS\_NIC\_交换机\_VPORT\_信息\_ARRAY\_枚举\_，则将返回连接到网络适配器上指定 PCI Express （PCIe）物理功能（PF）或虚拟功能（VF）的所有 VPorts 的信息。 PF 或 VF 由该结构的**AttachedFunctionId**成员指定。

    如果**AttachedFunctionId**成员设置为 NDIS\_PF\_函数\_ID，则返回所有 VPorts 的信息。 这包括附加到 PF 的默认 VPort。 如果**AttachedFunctionId**成员设置为有效的 VF 标识符，则将返回附加到指定 VF 的所有 VPorts 的信息。

    **注意**  从 Windows Server 2012 开始，只能将一个非默认的 VPort 附加到 VF。 但是，可以将多个 VPorts （包括默认的 VPort）附加到 PF。

     

-   如果**Flags**成员设置为零，则将返回连接到网络适配器上的 PF 或 VF 的所有 VPorts 的信息。 在这种情况下，将忽略**SwitchId**和**AttachedFunctionId**的值。

NDIS 为微型端口驱动程序[\_枚举\_VPORTS 请求处理 OID\_NIC\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   Oid [\_NIC\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)的 oid 方法请求。

-   OID [\_NIC\_SWITCH\_VPORT\_参数设置 oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)请求。

 

 





