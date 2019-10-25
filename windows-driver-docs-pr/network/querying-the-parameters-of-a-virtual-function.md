---
title: 查询虚拟功能的参数
description: 查询虚拟功能的参数
ms.assetid: D834762D-9141-4F0F-B76D-5C8ABB016B64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d14d13b42510146498045deb9ac21eb1ef71978e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844875"
---
# <a name="querying-the-parameters-of-a-virtual-function"></a>查询虚拟功能的参数


覆盖驱动程序或用户模式应用程序可以在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上获取 PCI Express （PCIe）虚拟功能（VF）的当前参数。 驱动程序或应用程序发出 OID\_NIC 的对象标识符（OID）方法请求[\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)以获取这些参数。

在过量驱动程序发出此 OID 方法请求之前，它必须[ **\_交换机\_VF\_参数结构初始化 NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters) 。 驱动程序或应用程序必须将**VFId**成员设置为要为其返回参数的 VF 的标识符。 可以通过以下方式获取 VF 标识符：

-   通过\_\_NIC 发出 oid 方法请求， [\_枚举\_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)。

    如果此 OID 请求成功完成，则过量驱动程序或用户模式应用程序将收到网络适配器上分配的所有 VFs 的列表。 列表中的每个元素都是一个[**NDIS\_NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)结构，以及由**VFId**成员指定的 vf 标识符。

-   通过向[\_分配\_VF\_\_NIC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)发出 OID 的 oid 方法请求。

    如果此 OID 请求成功完成，则过量驱动程序会在返回的 NDIS\_NIC 的**VFId**成员中接收新创建的 VF 的标识符[ **\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

    **请注意**  只有过量驱动程序才能以这种方式获取 VF 标识符。

     

成功从 OID 方法请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_NIC 的指针\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 此结构包含指定的 VF 的配置参数。

NDIS [\_NIC\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)请求用于微型端口驱动程序。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   Oid [\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)的 oid 方法请求。

-   OID\_NIC 上设置 Oid 的请求[\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)。

 

 





