---
title: NET_BUFFER_LIST 结构
description: NET_BUFFER_LIST 结构
ms.assetid: f7f19e48-cb63-458d-b175-6f99080e4cdf
keywords:
- NET_BUFFER_LIST
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
- 包 WDK 网络，数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec3c8bec093dcbc40cd7f70ecd49d54885f6d46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829057"
---
# <a name="net_buffer_list-structure"></a>NET\_BUFFER\_列表结构





[**Net\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构将网络\_缓冲结构的链接列表打包。

下图显示了网络\_缓冲区\_列表结构中的字段。

![说明 net\-buffer\-列表结构中的字段的关系图](images/netbufferlist.png)

NET\_BUFFER\_列表结构在**NetBufferListHeader**成员中包含一个[**网络\_缓冲区\_列表\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_header)结构。 NET\_BUFFER\_LIST\_标头结构在**NetBufferListData**成员中包含[**网络\_缓冲区\_列表\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_data)结构。 应使用 NDIS 宏来访问 NET\_BUFFER\_列表结构成员。 有关这些宏的详细信息，请参阅[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) structure 参考页。

某些成员仅由 NDIS 使用。 以下列表中定义了驱动程序最有可能使用的成员：

<a href="" id="parentnetbufferlist"></a>**ParentNetBufferList**  
如果网络\_缓冲区\_列表结构是派生自父项（克隆、分段或重新组合）的子级，则**ParentNetBufferList**指定指向父网络\_缓冲区\_列表结构的指针。 否则，此参数为**NULL**。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
指定一个池句柄，用于标识从中分配了 NET\_缓冲区\_列表结构的 NET\_缓冲区\_列表池。

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
保留以供协议驱动程序使用。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
保留供微型端口驱动程序使用。

<a href="" id="sourcehandle"></a>**SourceHandle**  
一个句柄，该句柄是通过使用下列驱动程序提供的例程之一在绑定或附加操作中为驱动程序提供的：

<a href="" id="miniport-driver"></a>微型端口驱动程序  
[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

<a href="" id="protocol-driver"></a>协议驱动程序  
[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

<a href="" id="filter-driver"></a>筛选器驱动程序  
[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

NDIS 使用**SourceHandle**将 NET\_缓冲区\_列表结构返回到发送 NET\_缓冲区\_列表结构的驱动程序。 NDIS 驱动程序不应读取此句柄。

<a href="" id="childrefcount"></a>**ChildRefCount**  
如果[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构是父级（具有由克隆、片段或重新组合操作派生的子项）， **ChildRefCount**将指定现有子级的数目。 否则，此参数为零。

<a href="" id="flags"></a>**随意**  
保留以供 NET\_缓冲区的属性的未来规范\_列表结构。 当前没有可供驱动程序使用的标志。

<a href="" id="status"></a>**状态值**  
指定此 NET\_缓冲区\_列表结构的网络数据操作的最终完成状态。 微型端口驱动程序在完成发送操作之前写入此值。

<a href="" id="netbufferlistinfo"></a>**NetBufferListInfo**  
指定列表中所有[**net\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构共有的[**net\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构信息。 此信息通常称为 "带外（OOB）数据"。

<a href="" id="next"></a>**一个**  
指定指向网络\_缓冲区\_列表结构的链接列表中的下一 NET\_缓冲区\_列表结构的指针。 如果网络\_缓冲区\_列表结构是列表中的最后一个结构，则该成员为**NULL**。

<a href="" id="firstnetbuffer"></a>**FirstNetBuffer**  
指定一个指针，该指针指向与此 NET\_缓冲区\_列表结构关联的网络\_缓冲区结构的链接列表中的第一个网络\_缓冲区结构。

**注释**  **上下文**是指向[**网络\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构的指针。 NDIS 提供宏和函数以便在**上下文**中处理数据。 有关 NET\_缓冲区\_列表\_上下文结构的详细信息，请参阅[net\_BUFFER\_list\_Context structure](net-buffer-list-context-structure.md)。

 

 

 





