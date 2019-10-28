---
title: 枚举虚拟端口上的接收筛选器
description: 枚举虚拟端口上的接收筛选器
ms.assetid: E809B7A3-256B-4351-8A60-D80D4A86EFDB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd84666d51a6e20825eef721be1c165a4cdcbb9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838118"
---
# <a name="enumerating-receive-filters-on-a-virtual-port"></a>枚举虚拟端口上的接收筛选器





在网络适配器的 NIC 交换机上创建虚拟端口（VPort）后，过量驱动程序和用户应用程序可以执行以下操作：

-   枚举 VPort 上的接收筛选器的参数。

    有关详细信息，请参阅[枚举接收筛选器](#enumerating-receive-filters)。

-   查询特定接收筛选器的参数。

    有关详细信息，请参阅[查询特定接收筛选器](#querying-a-specific-receive-filter)。

有关如何创建 VPort 的详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

## <a name="enumerating-receive-filters"></a>枚举接收筛选器


为了获取 NIC 交换机的虚拟端口（VPort）上设置的所有接收筛选器的列表，过量驱动程序和应用程序可以发出 OID 的对象标识符（OID）方法请求[\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**NDIS\_接收\_筛选器\_\_数组结构的筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)的指针。

在过量驱动程序或用户应用程序发出此 OID 方法请求之前，它必须初始化[**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构并按以下方式设置此结构的成员：

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_ID。

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   通过[oid\_NIC\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)的上一个 oid 方法请求\_CREATE\_VPORT。

    -   \_\_NIC 的上一个 OID 方法请求[\_枚举\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)。

    **请注意**  此成员仅在以下情况下有效：驱动程序或应用程序将 NDIS\_接收\_筛选器\_筛选器\_在**FLAGS**成员中指定的标志\_\_。 如果未设置此标志，则返回在 NIC 交换机上的每个 VPort 上设置的接收筛选器。

     

成功从 Oid 的 OID 方法请求返回[\_接收\_FILTER\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向已更新 Ndis\_的指针将[**接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，后面跟有一个或多个[**NDIS\_\_INFO 结构接收\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)。 每个**NDIS\_接收\_筛选器\_信息**结构指定在指定 VPort 上设置的接收筛选器的唯一标识符。

## <a name="querying-a-specific-receive-filter"></a>查询特定接收筛选器


过量驱动程序或应用程序可以[\_接收\_filter\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)发出 oid 方法请求，以获取 VPort 上特定筛选器的参数。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。

在过量驱动程序或用户应用程序发出此 OID 方法请求之前，它必须初始化[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，并按以下方式设置此结构的成员：

-   **FilterId**成员必须设置为要返回其参数的筛选器的非零标识符值。

    **请注意**  过量驱动程序从 oid 的早期 oid 方法请求中获取了筛选器标识符[\_接收\_筛选器\_设置\_筛选](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)器或 OID\_\_[枚举接收\_筛选器\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 应用程序只能从 OID 的早期 OID 方法请求中获取筛选器标识符\_接收\_FILTER\_枚举\_筛选器。

     

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_ID。

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   通过[oid\_NIC\_开关](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)的上一个 oid 方法请求\_CREATE\_VPORT。

    -   \_\_NIC 的上一个 OID 方法请求[\_枚举\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)。

NDIS 处理[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)和[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)方法 OID 请求用于微型端口驱动程序。 NDIS 从 OID 收到的数据的内部缓存获取信息[\_接收\_filter\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 请求。

 

 





