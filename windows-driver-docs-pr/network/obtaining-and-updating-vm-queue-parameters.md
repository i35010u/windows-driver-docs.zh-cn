---
title: 获取和更新 VM 队列参数
description: 获取和更新 VM 队列参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b622e539c7f4a82efa9d8cd02497de30229bea0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813671"
---
# <a name="obtaining-and-updating-vm-queue-parameters"></a>获取和更新 VM 队列参数





过量驱动程序可以在分配 VM 队列后设置其配置参数。 此外，过量驱动程序或应用程序可以获取队列的当前参数，以及在队列中设置的筛选器的参数。

若要更改队列的当前配置参数，过量驱动程序可以使用 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](./oid-receive-filter-queue-parameters.md) 设置 oid 请求。 过量驱动程序在 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员中提供了指向 [**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针。

\_ \_ \_ 在[oid 接收 \_ \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md)OID 和[oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](./oid-receive-filter-queue-parameters.md)OID 中使用 NDIS 接收队列参数结构。 有关分配队列的详细信息，请参阅 [分配 VM 队列](allocating-a-vm-queue.md)。

为了获取队列的当前配置参数，过量驱动程序可以使用 OID \_ 接收 \_ 筛选器 \_ 队列 \_ 参数方法 oid 请求。 最初， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构的指针，该结构具有类型为 ndis \_ 接收队列 ID 的队列标识符 \_ \_ 。 成功从 OID 方法请求返回后，NDIS OID 请求结构的 **InformationBuffer** 成员 \_ \_ 包含指向 **NDIS \_ 接收 \_ 队列 \_ 参数** 结构的指针。

NDIS 处理微型端口驱动程序的方法请求。 因此， \_ \_ \_ \_ 没有为微型端口驱动程序请求 oid 接收筛选器队列参数方法 oid 请求。 NDIS 从 OID \_ 接收 \_ 筛选器 \_ 分配 \_ 队列和 oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数 oid 请求中收到的数据的内部缓存获取信息。

为了获取接收队列中筛选器的当前配置参数，过量驱动程序可以使用 [oid \_ 接收 \_ 筛选器 \_ 参数](./oid-receive-filter-parameters.md) 方法 oid 请求。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员最初包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 NDIS 使用输入结构中的 **FilterId** 成员来确定筛选器。 成功从方法请求返回后，NDIS OID 请求结构的 **InformationBuffer** 成员 \_ \_ 包含指向已更新的 ndis \_ 接收 \_ 筛选器参数结构的指针 \_ 。

NDIS 处理 \_ \_ 微型端口驱动程序的 oid 接收筛选器 \_ 参数方法 oid 请求。 NDIS 从 [oid \_ 接收 \_ 筛选器 \_ 设置 \_ 筛选器](./oid-receive-filter-set-filter.md) oid 请求收到的数据的内部缓存获取了信息。

过量驱动程序可以使用 OID \_ 接收 \_ 筛选器 \_ 参数方法 oid 请求来获取接收队列中的筛选器的配置参数。

过量驱动程序从较早的 OID \_ 接收 \_ 筛选器 \_ 集筛选器 \_ 方法 Oid 请求或从 [oid \_ 接收筛选器 \_ \_ 枚举 \_ 筛选](./oid-receive-filter-enum-filters.md) 器 oid 请求获取筛选器标识符。 只有驱动程序才能使用 OID \_ 接收 \_ 筛选器 \_ 集 \_ 筛选请求。

应用程序从 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选](./oid-receive-filter-enum-filters.md) 器 oid 请求中获取了筛选器标识符。

 

