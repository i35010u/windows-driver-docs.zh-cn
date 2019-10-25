---
title: NET_BUFFER_LIST_CONTEXT 结构
description: NET_BUFFER_LIST_CONTEXT 结构
ms.assetid: 45be8503-2c5f-46e6-9fc3-b1b3c42f0d91
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
ms.openlocfilehash: f83ba51f94e0b39bc8efafe76be2ea6b5f06953d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844928"
---
# <a name="net_buffer_list_context-structure"></a>NET\_缓冲区\_列表\_上下文结构





NDIS 驱动程序使用[**net\_BUFFER\_list\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构来存储与[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构关联的附加数据。 NET\_缓冲区\_列表结构的**上下文**成员是指向网络\_缓冲区\_列表\_上下文结构的指针。 在网络\_缓冲区\_列表中存储的信息\_上下文结构对于堆栈中的 NDIS 和其他驱动程序是不透明的。

下图显示了网络\_缓冲区\_列表\_上下文结构中的字段。

![说明 net\-缓冲区中的字段的关系图\-列表\-上下文结构](images/netbufferlistcontext.png)

[**NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构包含包含上下文数据的**ContextData**成员。 此数据可以是驱动程序所需的任何上下文信息， [ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

驱动程序应使用以下 NDIS 宏和函数来访问和操作 NET\_缓冲区中的成员\_列表\_上下文结构：

[**NdisAllocateNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistcontext)

[**NdisFreeNetBufferListContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistcontext)

[**NET\_缓冲区\_列表\_上下文\_数据\_启动**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-start)

[**NET\_缓冲区\_列表\_上下文\_数据\_大小**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-context-data-size)

 

 





