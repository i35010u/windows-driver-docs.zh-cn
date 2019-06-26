---
title: NET_BUFFER_LIST_CONTEXT 结构
description: NET_BUFFER_LIST_CONTEXT 结构
ms.assetid: 45be8503-2c5f-46e6-9fc3-b1b3c42f0d91
keywords:
- NET_BUFFER_LIST_CONTEXT
- 网络数据 WDK，结构
- 数据 WDK 网络结构
- 数据包 WDK 网络、 数据结构
- 网络数据 WDK，上下文数据
- 数据 WDK 网络，上下文数据
- 数据包 WDK 网络的上下文数据
- 上下文 da
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8207ac2cd172ca4cb75cc216e5bbdc91f09a53ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379766"
---
# <a name="netbufferlistcontext-structure"></a>NET\_缓冲区\_列表\_上下文结构





使用 NDIS 驱动程序[ **NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构，以存储与之关联的其他数据[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 **上下文**NET 成员\_缓冲区\_列表结构是指向 NET\_缓冲区\_列表\_上下文结构。 在 NET 中存储的信息\_缓冲区\_列表\_上下文结构是不透明的 NDIS 和堆栈中的其他驱动程序。

下图显示字段在 NET\_缓冲区\_列表\_上下文结构。

![说明在网络中的字段的关系图\-缓冲区\-列表\-上下文结构](images/netbufferlistcontext.png)

[ **NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构包括**ContextData**包含上下文数据的成员。 此数据可以是驱动程序需要的任何上下文信息[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

驱动程序应使用以下 NDIS 宏和函数来访问和处理网络中的成员\_缓冲区\_列表\_上下文结构：

[**NdisAllocateNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistcontext)

[**NdisFreeNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlistcontext)

[**NET\_缓冲区\_列表\_上下文\_数据\_开始**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-start)

[**NET\_BUFFER\_LIST\_CONTEXT\_DATA\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-size)

 

 





