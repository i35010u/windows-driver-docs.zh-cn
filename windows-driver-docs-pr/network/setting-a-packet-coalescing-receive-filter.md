---
title: 设置数据包合并接收筛选器
description: 设置数据包合并接收筛选器
ms.assetid: 59BD092F-A530-446F-93E7-02E1F254E9A0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe304bb8d8041e910dbd737e684fe6264856864c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841960"
---
# <a name="setting-a-packet-coalescing-receive-filter"></a>设置数据包合并接收筛选器


若要在支持数据包合并的微型端口驱动程序上下载和设置接收筛选器，过量驱动程序会发出 oid [\_接收\_筛选器的 oid 方法请求\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)。 \_oid 的[**NDIS\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**Ndis\_接收\_筛选器，\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，用于指定 NDIS 接收筛选器的参数。

-   一组[**NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构，后者指定网络数据包标头中的字段的筛选器测试条件。

有关过量驱动程序如何为数据包合并接收筛选器指定参数的详细信息，请参阅[指定数据包合并接收筛选器](specifying-a-packet-coalescing-receive-filter.md)。

当 NDIS 收到 OID 请求来设置基础网络适配器上的接收筛选器时，它会验证接收筛选器参数。 如果过量驱动程序正在指定新的接收筛选器，NDIS 还将为接收筛选器生成唯一筛选器标识符（ID）。

在 NDIS 分配了所需的资源和筛选器 ID 后，它会将 OID 请求转发到微型端口驱动程序。 如果微型端口驱动程序可以成功分配接收筛选器所需的软件和硬件资源，微型端口驱动程序完成 OID 请求，状态为 NDIS\_状态\_SUCCESS。

成功从 Oid 的 OID 方法请求返回后[\_接收\_filter\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指针对于[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。 使用新的筛选器 ID 通过 NDIS 更新此结构。

 

 





