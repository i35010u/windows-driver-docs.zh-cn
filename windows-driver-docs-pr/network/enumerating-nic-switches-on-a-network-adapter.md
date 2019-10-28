---
title: 枚举网络适配器上的 NIC 交换机
description: 枚举网络适配器上的 NIC 交换机
ms.assetid: 0799A879-2BC0-43C5-A6B6-6D46C74A26FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b3f233238d95730000afffa430f0085dfd835c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838120"
---
# <a name="enumerating-nic-switches-on-a-network-adapter"></a>枚举网络适配器上的 NIC 交换机


过量驱动程序或用户应用程序可以获取在支持单一根 i/o 虚拟化（SR-IOV）的网络适配器上创建的所有 NIC 交换机的列表。 驱动程序或应用程序发出 OID\_NIC 的对象标识符（OID）查询请求[\_交换机\_枚举\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)来获取此列表。

成功从此 OID 请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向缓冲区的指针，该缓冲区包含以下内容：

-   [**NDIS\_NIC\_交换机\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构，该结构定义数组中的元素数目。

-   [**NDIS\_NIC 的数组\_交换机\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。 其中每个结构都包含有关在网络适配器上创建的单个 NIC 交换机的信息。

    **请注意**  如果网络适配器没有 nic 交换机，则驱动程序将 NDIS\_\_NIC 的**NumElements**成员设置为[ **\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构设置为零，而不将[**ndis\_NIC\_返回\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构的开关。

     

**注意**  从 Windows Server 2012 开始，sr-iov 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为*默认 NIC 交换机*，由 NDIS\_默认\_交换机\_ID 标识符引用。

 

NDIS 处理[\_NIC 的 OID\_交换机\_\_ENUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)驱动程序请求。 NDIS 从以下源中返回的数据的内部缓存返回信息：

-   注册表中的标准化 SR-IOV 关键字设置。 有关这些关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   Oid\_NIC 的 OID 请求[\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)和[OID\_nic\_SWITCH\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters)。

**请注意**  ndis 还在[**ndis\_BIND\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)和[**ndis\_FILTER\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)的**NicSwitchArray**成员中提供开关的枚举构造. 因此，过量协议和筛选器驱动程序不必[\_开关\_NIC 发出 OID，\_ENUM\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)请求来获取此信息。

 

 

 





