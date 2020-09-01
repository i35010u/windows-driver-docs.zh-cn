---
title: 枚举分配的队列
description: 枚举分配的队列
ms.assetid: 4566314b-ea6b-49e2-bc85-946ed303bc6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d1b3103314c6afdadffba7ef7be66b253b6d948
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209741"
---
# <a name="enumerating-the-allocated-queues"></a>枚举分配的队列





为了获取网络适配器上分配的所有接收队列的列表，过量驱动程序会发出 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列](./oid-receive-filter-enum-queues.md) 查询 oid 请求。 成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 接收 \_ 队列 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)结构的指针，该结构后跟每个队列的[**ndis \_ 接收 \_ 队列 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)结构。

NDIS \_ \_ \_ 为微型端口驱动程序处理 oid 接收筛选器枚举 \_ 队列查询 oid 请求。 NDIS 从 [oid \_ 接收 \_ 筛选器 \_ 分配 \_ 队列](./oid-receive-filter-allocate-queue.md) 和 [oid \_ 接收 \_ 筛选器 \_ 队列 \_ 参数](./oid-receive-filter-queue-parameters.md) oid 请求中收到的数据的内部缓存获取信息。

过量驱动程序和用户模式应用程序可以使用 OID \_ 接收 \_ 筛选器 \_ 枚举 \_ 队列 oid 查询请求来枚举网络适配器上的接收队列。

如果协议驱动程序发出请求，则将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的请求类型设置为 **NdisRequestQueryInformation** ，并且此 OID 返回在网络适配器上分配协议驱动程序的所有接收队列的数组。 如果用户模式应用程序发出了请求，则将 NDIS OID 请求中的请求类型 \_ \_ 设置为 **NdisRequestQueryStatistics**，并且此 OID 返回微型端口适配器上所有接收队列的信息数组。

 

