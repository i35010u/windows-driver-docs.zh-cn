---
title: 枚举网络适配器上的虚拟端口
description: 枚举网络适配器上的虚拟端口
ms.assetid: 437C3356-4CC7-4128-9E61-FD01157F4FD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06701942d6bad9570818358af5f9f9c021b7cab3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212499"
---
# <a name="enumerating-virtual-ports-on-a-network-adapter"></a>枚举网络适配器上的虚拟端口


覆盖驱动程序或用户应用程序可以在支持单一根 i/o 虚拟化 (SR-IOV) 的网络适配器的 NIC 交换机上获取 (VPorts) 的所有虚拟端口的列表。 驱动程序或应用程序发出对象标识符 (oid [ \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](./oid-nic-switch-enum-vports.md) 的 oid) 方法请求来获取此列表。

成功从此 OID 查询请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   用于定义数组中的元素数的 [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ INFO \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array) 结构。

-   [**NDIS \_ NIC \_ 交换机 \_ VPORT \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构的数组。 其中每个结构都包含有关网络适配器的 NIC 交换机上的 VPort 的信息。

    **注意**   如果未在网络适配器上创建 VPorts，则驱动程序会将[**ndis \_ nic \_ 交换机 \_ VPORT \_ INFO \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array)结构的**NumElements**成员设置为零，且不会返回[**ndis \_ nic \_ 交换机 \_ VPORT \_ INFO**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info)结构。

     

在过量的驱动程序或用户应用程序发出 [OID \_ nic \_ switch \_ ENUM \_ VPORTS](./oid-nic-switch-enum-vports.md) 请求之前，它必须初始化与请求一起传递的 [**NDIS \_ nic \_ 交换机 \_ VPORT \_ INFO \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_info_array) 结构。 当初始化 **NDIS \_ NIC \_ 交换机 \_ VPORT \_ INFO \_ 数组** 结构时，驱动程序或应用程序必须遵循以下准则：

-   如果在 \_ \_ \_ \_ \_ \_ Flags 成员中设置了特定交换机标志上的 NDIS NIC 交换机 VPORT INFO ARRAY ENUM \_ \_ ，则 \_ 会为指定 NIC 交换机上创建的所有 VPorts 返回信息。 **Flags** NIC 交换机由该结构的 **SwitchId** 成员指定。

    **注意**   从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 *默认 NIC 交换机*，由 NDIS \_ 默认 \_ 交换机 \_ ID 标识符引用。 不管 **flags** 成员中设置了哪些标志，都必须将 **SwitchId** 成员设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

     

-   如果在 \_ \_ \_ \_ \_ Flags 成员中设置了特定函数标志上的 "NDIS NIC 交换机 VPORT 信息数组 \_ 枚举"，则 \_ \_ \_ 会为附加到指定 PCI Express (PCIe) 物理函数 (PF) 或虚拟函数 (网络适配器上的虚拟功能) 虚拟功能的所有 VPorts 返回信息。 **Flags** PF 或 VF 由该结构的 **AttachedFunctionId** 成员指定。

    如果将 **AttachedFunctionId** 成员设置为 NDIS \_ PF \_ 函数 \_ ID，则将返回所有 VPorts 的信息。 这包括附加到 PF 的默认 VPort。 如果 **AttachedFunctionId** 成员设置为有效的 VF 标识符，则将返回附加到指定 VF 的所有 VPorts 的信息。

    **注意**   从 Windows Server 2012 开始，只能向 VF 附加一个非默认的 VPort。 但是，多个 VPorts (包括默认 VPort) 可以附加到 PF。

     

-   如果 **Flags** 成员设置为零，则将返回连接到网络适配器上的 PF 或 VF 的所有 VPorts 的信息。 在这种情况下，将忽略 **SwitchId** 和 **AttachedFunctionId** 的值。

NDIS 为微型端口驱动程序处理 [OID \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](./oid-nic-switch-enum-vports.md) 请求。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   [Oid \_ NIC \_ 交换器 \_ CREATE \_ VPORT](./oid-nic-switch-create-vport.md)的 oid 方法请求。

-   OID 设置 [oid \_ NIC \_ SWITCH \_ VPORT \_ 参数](./oid-nic-switch-vport-parameters.md)的请求。

 

