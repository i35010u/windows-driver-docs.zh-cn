---
title: 查询虚拟端口的参数
description: 查询虚拟端口的参数
ms.assetid: 482DA041-2C70-438A-8D29-0F338CDCF935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78e37bc1d220a3bcf044345759e986db7f12f8c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844874"
---
# <a name="querying-the-parameters-of-a-virtual-port"></a>查询虚拟端口的参数


过量驱动程序可以在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上的 NIC 交换机上获取虚拟端口（VPort）的参数。 驱动程序发出 OID\_NIC 的对象标识符（OID）方法请求[\_交换机\_VPORT\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)以获取这些参数。

在过量驱动程序发出此 OID 方法请求之前，它必须[ **\_交换机\_VPORT\_参数结构初始化 NDIS\_NIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 。 驱动程序必须按以下方式设置此结构的成员：

-   **SwitchId**成员必须设置为要为其返回参数的 NIC 交换机的标识符。

    **注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 "*默认 NIC 交换机*"。 **SwitchId**成员必须设置为 NDIS\_默认\_交换机\_ID。

     

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   通过[oid\_NIC\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)的上一个 oid 方法请求\_CREATE\_VPORT。

    -   \_\_NIC 的上一个 OID 方法请求[\_枚举\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)。

成功从此 OID 方法请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_NIC 的指针\_交换机\_VPORT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters)结构。 此结构包含指定 VPort 的参数。

NDIS 处理[\_NIC 的 OID\_交换机\_VPORT\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)请求以获得微型端口驱动程序。 NDIS 从检查以下源中返回的数据的内部缓存返回信息：

-   Oid [\_NIC\_交换机\_CREATE\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)的 oid 方法请求。

-   OID [\_NIC\_SWITCH\_VPORT\_参数设置 oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-vport-parameters)请求。

 

 





