---
title: 克隆的 NET_BUFFER_LIST 结构
description: 克隆的 NET_BUFFER_LIST 结构
ms.assetid: efcf7d03-401e-46da-9ca3-8423af1e385a
keywords:
- NET_BUFFER_LIST
- 克隆的结构 WDK 网络
- 重复结构 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e95998521adf3f1573b92bf3b127b62cc8cc2d95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373353"
---
# <a name="cloned-netbufferlist-structures"></a>克隆 NET\_缓冲区\_列表结构





NDIS 驱动程序创建的克隆[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构从现有的 NET\_缓冲区\_列表结构。 克隆的结构引用的原始结构数据。 驱动程序可以使用此类结构高效地将相同的数据传输到多个路径。

下图显示了父 NET 之间的关系\_缓冲区\_列表结构和克隆的子结构。

![说明 net 父级之间的关系的关系图\-缓冲区\-列表结构和克隆的子结构](images/netbufferlistclone.png)

上图中包含父[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构和派生自该父级的子结构。 父结构有一个[ **NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)结构和一个[ **NET\_缓冲区** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer) MDLs 附加结构。 父结构的父指针位于**NULL**指示它不派生的结构。

子 NET\_缓冲区\_列表结构有一个 NET\_MDLs 附加缓冲区结构。 子 NET\_缓冲区\_列表具有指向父结构的指针。 **NULL**其中 NET\_缓冲区\_列表\_上下文结构指针会指示子具有任何 NET\_缓冲区\_列表\_上下文结构。

驱动程序调用[ **NdisAllocateCloneNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateclonenetbufferlist)函数来创建克隆[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 新分配 NDIS [ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构和以克隆 NET MDLs\_缓冲区\_列表结构。 不会分配 NDIS [ **NET\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list_context)克隆结构的结构。 新的 NET\_缓冲区结构和 MDLs 描述与父结构相同的数据。 不复制数据。

驱动程序调用[ **NdisFreeCloneNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreeclonenetbufferlist)函数来释放 NET\_缓冲区\_列表结构以及所有关联的 NET\_缓冲区结构和 MDL通过调用以前分配的链**NdisAllocateCloneNetBufferList**。

## <a name="related-topics"></a>相关主题


[派生 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






