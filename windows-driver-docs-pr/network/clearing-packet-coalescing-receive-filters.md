---
title: 清除数据包合并接收筛选器
description: 清除数据包合并接收筛选器
ms.assetid: 0924A494-AA4E-45FA-AFE6-65E0D105E0F2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67eb0c8e475603329a99695b9d8ae5889ddd5f63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835174"
---
# <a name="clearing-packet-coalescing-receive-filters"></a>清除数据包合并接收筛选器


若要在支持数据包合并的微型端口驱动程序上免费或*清除*接收筛选器，则过量驱动程序会发出 OID [\_接收\_筛选器的 oid 集请求，\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_接收\_筛选器的指针，\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构。

过量驱动程序（如协议或筛选器驱动程序）初始化[**NDIS\_接收\_筛选器\_按以下方式清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构：

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_ID。

    **注意**  从 NDIS 6.30 开始，仅在网络适配器的默认接收队列中支持数据包合并接收筛选器。 此接收队列具有 NDIS\_默认\_接收\_队列\_ID 的标识符。

     

-   **FilterId**成员必须设置为要在微型端口驱动程序上清除的筛选器的非零标识符（ID）值。 过量驱动程序从 Oid 的早期 OID 方法请求中获取了筛选器 ID [\_接收\_filter\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)或 OID\_\_\_[枚举\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)筛选器。

    **请注意**  只有设置了包合并接收筛选器的过量驱动程序才能将其清除。

     

**请注意**  在完成取消绑定或分离操作之前，过量协议或筛选器驱动程序必须清除它在基础微型端口驱动程序上设置的所有数据包合并接收筛选器。

 

 

 





