---
title: 枚举分配的队列
description: 枚举分配的队列
ms.assetid: 4566314b-ea6b-49e2-bc85-946ed303bc6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9972e0512207d45e6cdcfaa5a08862868b9c6096
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354562"
---
# <a name="enumerating-the-allocated-queues"></a>枚举分配的队列





若要获取的所有接收队列的列表上分配网络适配器，基础驱动程序问题[OID\_接收\_筛选器\_枚举\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-queues)查询 OID 请求。 从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_队列\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info_array)结构，后跟[**NDIS\_接收\_队列\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info)结构为每个队列。

NDIS 处理 OID\_接收\_筛选器\_枚举\_队列查询 OID 请求微型端口驱动程序。 NDIS 从它来自数据的内部缓存中获取信息[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)和[OID\_接收\_筛选器\_队列\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)OID 请求。

过量驱动程序和用户模式应用程序可以使用 OID\_接收\_筛选器\_枚举\_队列 OID 查询请求，以枚举网络适配器上的接收队列。

如果协议驱动程序发出请求时，键入请求[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构设置为**NdisRequestQueryInformation**和此 OID 上的网络适配器返回的所有接收队列协议驱动程序分配的数组。 如果在用户模式应用程序发出的请求，请求键入 NDIS\_OID\_请求设置为**NdisRequestQueryStatistics**，和此 OID 上返回一个数组的所有接收队列的信息中的微型端口适配器。

 

 





