---
title: 克隆的 NET_BUFFER_LIST 结构
description: 克隆的 NET_BUFFER_LIST 结构
ms.assetid: efcf7d03-401e-46da-9ca3-8423af1e385a
keywords:
- NET_BUFFER_LIST
- 克隆的结构 WDK 网络
- 复制结构 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55c3d243366f31995270bd02386cb8abdb6cf72a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838204"
---
# <a name="cloned-net_buffer_list-structures"></a>克隆的 NET\_缓冲区\_列表结构





NDIS 驱动程序从现有 NET\_缓冲区\_列表结构创建克隆的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 克隆的结构引用原始结构数据。 驱动程序可以使用这种类型的结构有效地将相同的数据传输到多个路径。

下图显示了 parent\_缓冲区\_列表结构和克隆的子结构之间的关系。

![说明 parent\-缓冲区\-列表结构和克隆的子结构之间的关系的关系图](images/netbufferlistclone.png)

上图包含一个父[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和派生自该父对象的子结构。 父结构具有一个[**网络\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构和一个连接了 MDLs 的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 父结构的父指针为**NULL** ，表示它不是派生的结构。

子网\_缓冲区\_列表结构具有一个附加了 MDLs 的 NET\_缓冲区结构。 子网\_缓冲区\_列表包含指向父结构的指针。 如果**为 NULL** ，则 NET\_缓冲区\_列表\_上下文结构指针将指示子网中没有 NET\_缓冲区\_列表\_的上下文结构。

驱动程序调用[**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateclonenetbufferlist)函数来创建克隆[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 NDIS 将新的[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构和 MDLs 分配给克隆的 NET\_缓冲区\_列表结构。 对于克隆的结构，NDIS 不会[ **\_列表\_上下文结构分配 NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)。 新的 NET\_BUFFER 结构和 MDLs 描述与父结构相同的数据。 不会复制数据。

驱动程序调用[**NdisFreeCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeclonenetbufferlist)函数，以释放以前通过调用**进行分配的网络\_缓冲区\_列表结构和所有关联的 net\_缓冲结构和 MDL 链NdisAllocateCloneNetBufferList**。

## <a name="related-topics"></a>相关主题


[派生的 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






