---
title: 筛选器驱动程序缓冲区管理
description: 筛选器驱动程序缓冲区管理
ms.assetid: 92b38710-056d-4853-b266-ca86cee298b6
keywords:
- 筛选器驱动程序 WDK 网络缓冲区
- NDIS 筛选器驱动程序 WDK，缓冲区
- 缓冲区管理 WDK NDIS 筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb56bf78d8ad429d0d806cc02222e09954102a3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353733"
---
# <a name="filter-driver-buffer-management"></a>筛选器驱动程序缓冲区管理





筛选器驱动程序创建的缓冲区复制其他驱动程序，从获取网络数据，或者要启动发送或接收操作。

如果筛选器驱动程序不会创建缓冲区，该驱动程序不会管理缓冲池。 这样的驱动程序只需将它从其他驱动程序收到的缓冲区上传递。

创建缓冲区以支持发送或接收操作的筛选器驱动程序必须管理[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构池并[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构池。

若要创建这些池，驱动程序，请调用以下函数：

[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)

[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferpool)

筛选器驱动程序可以使用以下函数来从池中分配结构：

[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)

[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlist)

[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbuffer)

调用**NdisAllocateNetBufferAndNetBufferList**比调用效率更高**NdisAllocateNetBufferList**跟**NdisAllocateNetBuffer**。 但是， **NdisAllocateNetBufferAndNetBufferList**只会创建一个 NET\_缓冲区结构的网上\_缓冲区\_列表结构。 若要使用**NdisAllocateNetBufferAndNetBufferList**，该驱动程序必须设置*AllocateNetBuffer*参数**TRUE**当调用**NdisAllocateNetBufferListPool**。

筛选器驱动程序发出的发送请求应确定基础驱动程序的上下文和回填空间要求。 筛选器驱动程序使用重新启动以确定基础驱动程序的回填要求的属性。 筛选器驱动程序应确定中的回填和上下文要求*正在重新启动*状态。 该驱动程序应为整个堆栈分配足够的回填和上下文空间。 如果有必要，筛选器驱动程序可以可用池，并重新分配其*正在重新启动*状态。

筛选器驱动程序使用以下函数可用池：

[**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlistpool)

[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferpool)

筛选器驱动程序使用以下函数以释放从池中分配的结构：

[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlist)

[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer)

驱动程序应释放 NET\_缓冲区结构分配带有**NdisAllocateNetBuffer**之前释放相关联的 NET\_缓冲区\_列表结构。 NET\_缓冲区结构分配带有**NdisAllocateNetBufferAndNetBufferList**时，驱动程序调用释放**NdisFreeNetBufferList**于关联的网络\_缓冲区\_列表结构。

 

 





