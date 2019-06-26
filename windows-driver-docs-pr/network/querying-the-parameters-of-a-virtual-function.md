---
title: 查询虚拟功能的参数
description: 查询虚拟功能的参数
ms.assetid: D834762D-9141-4F0F-B76D-5C8ABB016B64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6313b4ebac5078c8abe526d2d0d9c60c9a5b98e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379194"
---
# <a name="querying-the-parameters-of-a-virtual-function"></a>查询虚拟功能的参数


基础驱动程序或用户模式应用程序可以获取当前参数的 PCI Express (PCIe) 虚拟函数 (VF) 上支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器。 驱动程序或应用程序发出的对象标识符 (OID) 方法请求[OID\_NIC\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)来获取这些参数。

基础驱动程序将发出此 OID 方法请求之前，必须将格式化[ **NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 驱动程序或应用程序必须设置**VFId**成员添加到为其参数是要返回的 VF 的标识符。 可以按以下方式获取 VF 标识符：

-   通过发出的 OID 方法请求[OID\_NIC\_交换机\_枚举\_VFS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vfs)。

    如果已成功完成此 OID 请求，则基础驱动程序或用户模式应用程序接收所有 VFs 上的网络适配器分配的列表。 在列表中的每个元素均[ **NDIS\_NIC\_交换机\_VF\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_info)的结构，其中指定VF标识符**VFId**成员。

-   通过发出的 OID 方法请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

    如果已成功完成此 OID 请求，则基础驱动程序接收的标识符中新创建的 VF **VFId**所返回的成员[ **NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。

    **请注意**  仅过量驱动程序可以获取这种方式中的取景器标识符。

     

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_NIC\_交换机\_VF\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_vf_parameters)结构。 此结构包含有关指定 VF 配置参数。

NDIS 句柄[OID\_NIC\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)微型端口驱动程序的请求。 NDIS 从它所维护从检查以下源的数据的内部缓存中返回的信息：

-   OID 的方法请求[OID\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

-   设置的请求通过 OID [OID\_NIC\_交换机\_VF\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vf-parameters)。

 

 





