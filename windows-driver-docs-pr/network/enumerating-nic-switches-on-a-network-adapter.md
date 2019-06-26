---
title: 枚举网络适配器上的 NIC 交换机
description: 枚举网络适配器上的 NIC 交换机
ms.assetid: 0799A879-2BC0-43C5-A6B6-6D46C74A26FB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5df966facc4cdba87e698bd9bac9853ff66ede2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354580"
---
# <a name="enumerating-nic-switches-on-a-network-adapter"></a>枚举网络适配器上的 NIC 交换机


基础驱动程序或用户应用程序可以获取已在支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器创建的所有 NIC 交换机的列表。 驱动程序或应用程序发出的对象标识符 (OID) 查询请求[OID\_NIC\_交换机\_枚举\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)来获取此列表。

通过此 OID 请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指向包含如下内容的缓冲区：

-   [ **NDIS\_NIC\_交换机\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)结构，用于定义数组中元素数。

-   一个数组[ **NDIS\_NIC\_交换机\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_info)结构。 每个这些结构包含有关网络适配器上创建一个 NIC 交换机的信息。

    **请注意**  如果网络适配器不具有任何 NIC 开关，该驱动程序集**NumElements**的成员[ **NDIS\_NIC\_交换机\_INFO\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_delete_vport_parameters)为零，并无结构[ **NDIS\_NIC\_交换机\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_info)返回的结构。

     

**请注意**  从 Windows Server 2012 开始，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

 

NDIS 句柄[OID\_NIC\_交换机\_枚举\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)微型端口驱动程序的请求。 NDIS 从它所维护以下来源的数据的内部缓存中返回的信息：

-   在注册表中的标准化的 SR-IOV 关键字设置。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   OID 请求[OID\_NIC\_交换机\_创建\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-switch)并[OID\_NIC\_交换机\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-parameters).

**请注意**  NDIS 还提供了枚举中的交换机**NicSwitchArray**中的成员[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)并[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 因此，如果选择的协议和筛选器驱动程序没有颁发[OID\_NIC\_交换机\_枚举\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-switches)请求获取此信息。

 

 

 





