---
title: 枚举网络适配器上的虚拟功能
description: 枚举网络适配器上的虚拟功能
ms.assetid: 3AAF2D8B-9C7A-4E5B-86B6-264ACA5EA492
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9a357db300a91edfe5bd69c8f15d68bddcf8451
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206107"
---
# <a name="enumerating-virtual-functions-on-a-network-adapter"></a>枚举网络适配器上的虚拟功能


覆盖驱动程序或用户应用程序可以在支持单一根 i/o 虚拟化 (SR-IOV) 的网络适配器上，获取所有 PCI Express (PCIe) 虚功能)  (的虚拟功能的列表。 驱动程序或应用程序发出对象标识符 (oid [ \_ NIC \_ 交换机 \_ 枚举 \_ VFS](./oid-nic-switch-enum-vfs.md) 的) 方法请求，以获取此列表。

在驱动程序或应用程序发出 OID 请求之前，它必须初始化与请求一起传递的 [**NDIS \_ NIC \_ 交换机 \_ VF \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array) 结构。 初始化 **NDIS \_ NIC \_ 交换机 \_ VF \_ 信息 \_ 阵列** 结构时，驱动程序或应用程序必须遵循以下准则：

-   如果在 \_ \_ \_ \_ \_ \_ Flags 成员中设置了特定交换机标志上的 NDIS NIC 交换机 VF 信息阵列枚举 \_ \_ ，则 \_ 过量驱动程序或应用程序必须将**SwitchId**成员设置为 sr-iov 网络适配器上 NIC 交换机的标识符。 **Flags** 通过以这种方式设置这些成员，只会为 SR-IOV 网络适配器上指定的 NIC 交换机返回 VF 信息。

    **注意**  过量驱动程序和用户模式应用程序可以通过发出 oid [ \_ nic \_ 交换机 \_ 枚举 \_ 开关](./oid-nic-switch-enum-switches.md)的 oid 查询请求来获取 NIC 交换机标识符。

-   如果 **Flags** 成员设置为零，则驱动程序或应用程序必须将 **SwitchId** 成员设置为零。 通过以这种方式设置这些成员，将为 SR-IOV 网络适配器上的所有 NIC 交换机返回 VF 信息。

    **注意**  从 Windows Server 2012 开始，Windows 只支持网络适配器上的默认 NIC 交换机。 不管 **flags** 成员中的标志集如何，都必须将 **SwitchId** 成员设置为 NDIS \_ 默认 \_ 交换机 \_ ID。

成功从此 OID 查询请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向缓冲区的指针，该缓冲区包含以下内容：

-   用于定义数组中的元素数的 [**NDIS \_ NIC \_ 开关 \_ VF \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array) 结构。

-   [**NDIS \_ NIC \_ 交换机 \_ VF \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构的数组。 其中每个结构都包含有关网络适配器的 NIC 交换机上单个 VF 的信息。 通过 oid [ \_ nic \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的 oid 方法请求，将 VF 附加到 NIC 开关。

    **注意** 如果网络适配器上没有连接到任何一个 NIC 交换机的 VFs， [**ndis \_ nic \_ 交换机 \_ vf \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info_array)结构的**NumElements**成员将设置为零，且不会返回任何[**NDIS \_ nic \_ 交换机 \_ vf \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构。

    有关 NIC 交换机的详细信息，请参阅 [Nic 交换机](nic-switches.md)。

NDIS 为微型端口驱动程序处理 [OID \_ NIC \_ 交换机 \_ 枚举 \_ VFS](./oid-nic-switch-enum-vfs.md) 请求。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   Oid NIC 交换机的 OID 方法请求 [ \_ \_ \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)。

-   Oid 设置 [oid \_ NIC \_ 开关 \_ VF \_ 参数](./oid-nic-switch-vf-parameters.md)的请求。