---
title: 枚举虚拟端口上的接收筛选器
description: 枚举虚拟端口上的接收筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f6895aabafec1173162a8eea1a5a97b7109c0ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823909"
---
# <a name="enumerating-receive-filters-on-a-virtual-port"></a>枚举虚拟端口上的接收筛选器





在网络适配器的 NIC 交换机上创建虚拟端口 (VPort) 后，过量驱动程序和用户应用程序可以执行以下操作：

-   枚举 VPort 上的接收筛选器的参数。

    有关详细信息，请参阅 [枚举接收筛选器](#enumerating-receive-filters)。

-   查询特定接收筛选器的参数。

    有关详细信息，请参阅 [查询特定接收筛选器](#querying-a-specific-receive-filter)。

有关如何创建 VPort 的详细信息，请参阅 [创建虚拟端口](creating-a-virtual-port.md)。

## <a name="enumerating-receive-filters"></a>枚举接收筛选器


为了获取在 NIC 交换机 (VPort) 上设置的所有接收筛选器的列表，过量驱动程序和应用程序可以发出对象标识符 (OID) 方法请求 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员最初包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针。

在过量驱动程序或用户应用程序发出此 OID 方法请求之前，它必须初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array) 结构并按以下方式设置此结构的成员：

-   **QueueId** 成员必须设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

-   **VPortId** 成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   从 Oid NIC 交换机的上一个 OID 方法请求 [ \_ \_ \_ 创建 \_ VPORT](./oid-nic-switch-create-vport.md)。

    -   从 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](./oid-nic-switch-enum-vports.md)的上一个 oid 方法请求开始。

    **注意** 仅当驱动程序或应用程序在 \_ Flags 成员中设置 NDIS 接收 \_ 筛选器 \_ 信息 \_ 数组 \_ VPORT \_ ID \_ 指定标志 **Flags** 时，此成员才有效。 如果未设置此标志，则返回在 NIC 交换机上的每个 VPort 上设置的接收筛选器。

     

成功从 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的 Oid 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向已更新的 [**ndis \_ 接收 \_ 筛选 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构的指针，该结构后跟一个或多个 [**NDIS \_ 接收 \_ 筛选器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info)结构。 每个 **NDIS \_ 接收 \_ 筛选器 \_ 信息** 结构指定在指定的 VPort 上设置的接收筛选器的唯一标识符。

## <a name="querying-a-specific-receive-filter"></a>查询特定接收筛选器


过量驱动程序或应用程序可以发出 Oid 方法请求，以在 VPort 上获取特定筛选器的参数 [ \_ \_ \_ ](./oid-receive-filter-parameters.md) 。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员最初包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。

在过量驱动程序或用户应用程序发出此 OID 方法请求之前，它必须初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构，并按以下方式设置此结构的成员：

-   **FilterId** 成员必须设置为要返回其参数的筛选器的非零标识符值。

    **注意**  过量驱动程序从 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器或 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选](./oid-receive-filter-enum-filters.md)器的早期 OID 方法请求中获取了筛选器标识符。 应用程序只能从 OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器的早期 oid 方法请求中获取筛选器标识符。

     

-   **QueueId** 成员必须设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

-   **VPortId** 成员必须设置为与 VPort 关联的标识符。 过量驱动程序通过以下方式之一获取 VPort 标识符：

    -   从 Oid NIC 交换机的上一个 OID 方法请求 [ \_ \_ \_ 创建 \_ VPORT](./oid-nic-switch-create-vport.md)。

    -   从 [oid \_ NIC \_ 交换机 \_ 枚举 \_ VPORTS](./oid-nic-switch-enum-vports.md)的上一个 oid 方法请求开始。

NDIS 为微型端口驱动程序处理 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md) 和 [oid \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md) 方法 oid 请求。 NDIS 从 [oid \_ 接收 \_ 筛选器 \_ 设置 \_ 筛选器](./oid-receive-filter-set-filter.md) oid 请求收到的数据的内部缓存获取了信息。

 

