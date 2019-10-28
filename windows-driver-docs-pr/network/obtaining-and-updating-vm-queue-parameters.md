---
title: 获取和更新 VM 队列参数
description: 获取和更新 VM 队列参数
ms.assetid: 42beceec-95ae-48e3-985f-b6ee8a84d68b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83b49e4639050abe1cdf8e2b1dbf1c385110ef9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837745"
---
# <a name="obtaining-and-updating-vm-queue-parameters"></a>获取和更新 VM 队列参数





过量驱动程序可以在分配 VM 队列后设置其配置参数。 此外，过量驱动程序或应用程序可以获取队列的当前参数，以及在队列中设置的筛选器的参数。

若要更改队列的当前配置参数，过量驱动程序可以使用[OID\_接收\_筛选器\_队列\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)设置 OID 请求。 过量驱动程序提供了一个指向 Ndis\_的指针，该指针在[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**INFORMATIONBUFFER**成员中[**接收\_QUEUE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)结构。

NDIS\_接收\_队列\_参数结构用于[OID\_接收\_筛选器\_分配\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)OID 和 OID\_\_\_\_[队列参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters)OID。 有关分配队列的详细信息，请参阅[分配 VM 队列](allocating-a-vm-queue.md)。

为了获取队列的当前配置参数，过量驱动程序可以使用 OID\_接收\_筛选器\_队列\_参数方法 OID 请求。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**ndis\_接收\_队列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)的指针，\_参数结构的队列标识符类型为 NDIS\_接收\_队列\_ID。 成功从 OID 方法请求返回后，NDIS\_OID\_请求结构的**InformationBuffer**成员包含指向**ndis\_接收\_队列\_参数**结构的指针。

NDIS 处理微型端口驱动程序的方法请求。 因此，不会为微型端口驱动程序请求 OID\_接收\_筛选器\_队列\_参数方法 OID 请求。 NDIS 从 OID 收到的数据的内部缓存获取信息\_接收\_筛选器\_分配\_队列和 OID\_接收\_筛选器\_队列\_参数 OID 请求。

为了获取接收队列中筛选器的当前配置参数，过量驱动程序可以使用[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)方法 OID 请求。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 NDIS 使用输入结构中的**FilterId**成员来确定筛选器。 成功从方法请求返回后，NDIS\_OID\_请求结构的**InformationBuffer**成员包含指向已更新 NDIS\_接收\_筛选器\_参数结构的指针。

NDIS 处理 OID\_接收\_筛选器\_参数方法 OID 请求用于微型端口驱动程序。 NDIS 从 OID 收到的数据的内部缓存获取信息[\_接收\_filter\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 请求。

过量驱动程序可以使用 OID\_接收\_FILTER\_参数方法 OID 请求，以获取接收队列中的筛选器的配置参数。

过量驱动程序从较早的 OID 获取筛选器标识符\_接收\_筛选器\_设置\_筛选器方法 OID 请求，或从[OID\_接收\_筛选器\_枚举](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)需要. 只有驱动程序才能使用 OID\_接收\_筛选器\_设置\_筛选请求。

应用程序从 Oid 获取筛选器标识符[\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)OID 请求。

 

 





