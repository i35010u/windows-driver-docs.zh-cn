---
title: 清除数据包合并接收筛选器
description: 清除数据包合并接收筛选器
ms.assetid: 0924A494-AA4E-45FA-AFE6-65E0D105E0F2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f831576d7bdd6f02a84e60a69b89e2e53d869d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385523"
---
# <a name="clearing-packet-coalescing-receive-filters"></a>清除数据包合并接收筛选器


若要释放，或*清除*，支持数据包合并的微型端口驱动程序上的接收筛选器，基础驱动程序发出的 OID 集请求[OID\_接收\_筛选器\_清除\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-clear-filter)。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构。

基础驱动程序，如协议或筛选器驱动程序，初始化[ **NDIS\_接收\_筛选器\_清除\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构按以下方式：

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_id。

    **请注意**  从 NDIS 6.30 开始，数据包合并接收筛选器仅支持在默认接收的网络适配器的队列。 此接收队列具有的 NDIS 标识符\_默认\_接收\_队列\_id。

     

-   **FilterId**成员都必须设置为非零值的标识符 (ID) 值的筛选器以在微型端口驱动程序时清除。 基础驱动程序从较早的 OID 方法请求获取筛选器 ID [OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)或者[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。

    **请注意**  仅设置数据包合并接收筛选器的基础驱动程序可将其清除。

     

**请注意**  完成解除绑定或分离操作之前，过量的协议或筛选器驱动程序必须清除所有数据包合并接收其基础的微型端口驱动程序设置的筛选器。

 

 

 





