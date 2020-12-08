---
title: NET_BUFFER_LIST_CONTEXT 结构
description: NET_BUFFER_LIST_CONTEXT 结构
keywords:
- NET_BUFFER_LIST_CONTEXT
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
- 包 WDK 网络，数据结构
- 网络数据 WDK，上下文数据
- 数据 WDK 网络，上下文数据
- 包 WDK 网络，上下文数据
- 上下文 da
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1dd253d2acce75bc2d88f3ac518d8b126ef3e01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805215"
---
# <a name="net_buffer_list_context-structure"></a>网络 \_ 缓冲区 \_ 列表 \_ 上下文结构





NDIS 驱动程序使用 [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构来存储与 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构关联的附加数据。 NET **Context** \_ buffer 列表结构的上下文成员 \_ 是指向网络 \_ 缓冲区 \_ 列表 \_ 上下文结构的指针。 网络 \_ 缓冲区列表上下文结构中存储的信息 \_ \_ 对于堆栈中的 NDIS 和其他驱动程序是不透明的。

下图显示了网络 \_ 缓冲区 \_ 列表上下文结构中的字段 \_ 。

![阐释网络 \- 缓冲区 \- 列表 \- 上下文结构中的字段的关系图](images/netbufferlistcontext.png)

[**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构包含包含上下文数据的 **ContextData** 成员。 此数据可以是驱动程序需要用于 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的任何上下文信息。

驱动程序应使用以下 NDIS 宏和函数来访问和操作网络 \_ 缓冲区 \_ 列表上下文结构中的成员 \_ ：

[**NdisAllocateNetBufferListContext**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistcontext)

[**NdisFreeNetBufferListContext**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistcontext)

[**网络 \_ 缓冲区 \_ 列表 \_ 上下文 \_ 数据 \_ 开始**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_context_data_start)

[**网络 \_ 缓冲区 \_ 列表 \_ 上下文 \_ 数据 \_ 大小**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_context_data_size)

 

