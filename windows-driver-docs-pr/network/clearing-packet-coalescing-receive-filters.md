---
title: 清除数据包合并接收筛选器
description: 清除数据包合并接收筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9edadc6814196d683da52582994c237c8e501d4
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248245"
---
# <a name="clearing-packet-coalescing-receive-filters"></a>清除数据包合并接收筛选器


若要在支持数据包合并的微型端口驱动程序上免费或 *清除* 接收筛选器，则过量驱动程序会发出 oid 请求，即 [oid \_ 接收 \_ 筛选 \_ \_ 器清除筛选器](./oid-receive-filter-clear-filter.md)。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ CLEAR \_ PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters)结构的指针。

使用过量驱动程序（如协议或筛选器驱动程序），按以下方式初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 清除 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_clear_parameters) 结构：

-   **QueueId** 成员必须设置为 NDIS \_ 默认 \_ 接收 \_ 队列 \_ ID。

    **注意**  从 NDIS 6.30 开始，仅在网络适配器的默认接收队列中支持数据包合并接收筛选器。 此接收队列具有 NDIS \_ 默认 \_ 接收 \_ 队列 ID 的标识符 \_ 。

     

-   **FilterId** 成员必须设置为要在微型端口驱动程序上清除的筛选器 (ID) 值的非零标识符。 过量驱动程序从 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选](./oid-receive-filter-set-filter.md) 器或 [oid \_ 接收 \_ 筛选器 \_ 枚举 \_ 筛选器](./oid-receive-filter-enum-filters.md)的早期 OID 方法请求获取了筛选器 ID。

    **注意**  只有设置了数据包合并接收筛选器的过量驱动程序才能将其清除。

     

**注意**  在完成取消绑定或分离操作之前，过量协议或筛选器驱动程序必须清除它在基础微型端口驱动程序上设置的所有数据包合并接收筛选器。

 

 

