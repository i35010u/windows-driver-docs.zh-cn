---
title: 枚举分配的队列
description: 枚举分配的队列
ms.assetid: 4566314b-ea6b-49e2-bc85-946ed303bc6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76a20db72c0d3eac0727b51d0b3138545fd6cac6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834773"
---
# <a name="enumerating-the-allocated-queues"></a>枚举分配的队列





为了获取网络适配器上分配的所有接收队列的列表，过量驱动程序[会发出 OID\_接收\_筛选器\_枚举\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)查询 OID 请求。 成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中的**InformationBuffer**成员包含指向[**ndis\_接收\_队列的指针\_\_的数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)结构，后跟[**NDIS\_接收**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)每个队列\_信息结构的\_队列。

NDIS 处理 OID\_接收\_筛选器\_枚举\_对微型端口驱动程序的查询 OID 请求进行排队。 NDIS 从 OID 收到的数据的内部缓存获取信息[\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)和 OID\_\_\_\_的[参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)OID 请求。

过量驱动程序和用户模式应用程序可以使用 OID\_接收\_筛选器\_枚举\_队列 OID 查询请求来枚举网络适配器上的接收队列。

如果协议驱动程序发出请求， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中的请求类型设置为**NdisRequestQueryInformation** ，并且此 OID 返回协议驱动程序在其上分配的所有接收队列的数组网络适配器。 如果用户模式应用程序发出了请求，NDIS\_OID\_请求中的请求类型设置为**NdisRequestQueryStatistics**，并且此 OID 返回微型端口适配器上所有接收队列的信息的数组。

 

 





