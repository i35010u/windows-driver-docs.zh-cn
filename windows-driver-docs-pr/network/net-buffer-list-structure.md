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
ms.openlocfilehash: ebc8e5646a7367b5f96f9d6754af85c631cdd589
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217251"
---
# <a name="net_buffer_list-structure"></a>网络 \_ 缓冲区 \_ 列表结构





[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构对网络缓冲区结构的链接列表进行打包 \_ 。

下图显示了网络 \_ 缓冲区列表结构中的字段 \_ 。

![阐释网络 \- 缓冲区列表结构中的字段的关系图 \-](images/netbufferlist.png)

NET \_ buffer \_ list 结构包含**NetBufferListHeader**成员中的[**网络 \_ 缓冲区 \_ 列表 \_ 标头**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_header)结构。 网络 \_ 缓冲区 \_ 列表 \_ 标头结构包含**NetBufferListData**成员中的[**网络 \_ 缓冲区 \_ 列表 \_ 数据**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_data)结构。 应使用 NDIS 宏来访问 NET \_ BUFFER \_ LIST 结构成员。 有关这些宏的详细信息，请参阅 [**NET \_ BUFFER \_ LIST**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) structure 参考页。

某些成员仅由 NDIS 使用。 以下列表中定义了驱动程序最有可能使用的成员：

<a href="" id="parentnetbufferlist"></a>**ParentNetBufferList**  
如果网络 \_ 缓冲区 \_ 列表结构是从父 (克隆、分段或重新组合) 派生的子，则 **ParentNetBufferList** 指定一个指向父级网络 \_ 缓冲区 \_ 列表结构的指针。 否则，此参数为 **NULL**。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
指定一个池句柄，用于标识 \_ \_ 从其 \_ 分配网络缓冲区列表结构的网络缓冲区列表池 \_ 。

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
保留以供协议驱动程序使用。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
保留供微型端口驱动程序使用。

<a href="" id="sourcehandle"></a>**SourceHandle**  
一个句柄，该句柄是通过使用下列驱动程序提供的例程之一在绑定或附加操作中为驱动程序提供的：

<a href="" id="miniport-driver"></a>微型端口驱动程序  
[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

<a href="" id="protocol-driver"></a>协议驱动程序  
[*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

<a href="" id="filter-driver"></a>筛选器驱动程序  
[*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

NDIS 使用 **SourceHandle** 将网络 \_ 缓冲区 \_ 列表结构返回到发送网络 \_ 缓冲区列表结构的驱动程序 \_ 。 NDIS 驱动程序不应读取此句柄。

<a href="" id="childrefcount"></a>**ChildRefCount**  
如果 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构为父 (包含由克隆、片段或重组操作派生的子) ， **ChildRefCount** 将指定现有子级的数目。 否则，此参数为零。

<a href="" id="flags"></a>**随意**  
保留以供将来用于网络 \_ 缓冲区列表结构的属性指定 \_ 。 当前没有可供驱动程序使用的标志。

<a href="" id="status"></a>**状态值**  
指定此网络 \_ 缓冲区列表结构的网络数据操作的最终完成状态 \_ 。 微型端口驱动程序在完成发送操作之前写入此值。

<a href="" id="netbufferlistinfo"></a>**NetBufferListInfo**  
指定列表中所有[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构通用的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构信息。 此信息通常称为 "带外 (OOB) 数据"。

<a href="" id="next"></a>**一个**  
指定一个指针，该指针指向 \_ \_ 网络 \_ 缓冲区列表结构的链接列表中的下一个网络缓冲区列表结构 \_ 。 如果网络 \_ 缓冲区 \_ 列表结构是列表中的最后一个结构，则该成员为 **NULL**。

<a href="" id="firstnetbuffer"></a>**FirstNetBuffer**  
指定一个指针，该指针指向 \_ \_ 与此网络 \_ 缓冲区列表结构关联的网络缓冲区结构的链接列表中的第一个网络缓冲区结构 \_ 。

**注释**  **上下文** 是指向 [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构的指针。 NDIS 提供宏和函数以便在 **上下文** 中处理数据。 有关网络 \_ 缓冲区 \_ 列表上下文结构的详细信息 \_ ，请参阅 [网络 \_ 缓冲区 \_ 列表 \_ 上下文结构](net-buffer-list-context-structure.md)。

 

 

