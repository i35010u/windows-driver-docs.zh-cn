---
title: 设置数据包合并接收筛选器
description: 设置数据包合并接收筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a3b89e88d8a956845efb4c5122747e0cddd736c
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247909"
---
# <a name="setting-a-packet-coalescing-receive-filter"></a>设置数据包合并接收筛选器


为了在支持数据包合并的微型端口驱动程序上下载和设置接收筛选器，过量驱动程序会发出 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 oid 方法请求。 OID 请求的 [**NDIS \_ oid \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   用于指定 NDIS 接收筛选器参数的 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) 结构。

-   用于指定网络数据包标头中的字段筛选器测试条件的 [**NDIS \_ 接收 \_ 筛选器 \_ 字段 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters) 结构的数组。

有关过量驱动程序如何为数据包合并接收筛选器指定参数的详细信息，请参阅 [指定数据包合并接收筛选器](specifying-a-packet-coalescing-receive-filter.md)。

当 NDIS 收到 OID 请求来设置基础网络适配器上的接收筛选器时，它会验证接收筛选器参数。 如果过量驱动程序指定新的接收筛选器，NDIS 还将为接收筛选器生成唯一的筛选器标识符 (ID) 。

在 NDIS 分配了所需的资源和筛选器 ID 后，它会将 OID 请求转发到微型端口驱动程序。 如果微型端口驱动程序可以成功分配接收筛选器所需的软件和硬件资源，微型端口驱动程序完成 OID 请求，状态为 NDIS \_ 状态 \_ 成功。

成功从 [oid \_ 接收 \_ 筛选器 \_ 集 \_ 筛选器](./oid-receive-filter-set-filter.md)的 Oid 方法请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构的指针。 使用新的筛选器 ID 通过 NDIS 更新此结构。

 

