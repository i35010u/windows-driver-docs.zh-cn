---
title: 协议驱动程序缓冲区管理
description: 协议驱动程序缓冲区管理
ms.assetid: 1f91b58e-d432-46c8-994e-d95c3aadfe43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc98252c95ca6cc943469e9c210af41e40330b5e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215172"
---
# <a name="protocol-driver-buffer-management"></a>协议驱动程序缓冲区管理





协议驱动程序必须管理 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构池和 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构池，以便发送操作。 若要创建这些池，驱动程序将调用以下函数：

[**NdisAllocateNetBufferListPool**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)

[**NdisAllocateNetBufferPool**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool)

协议驱动程序可以使用以下函数从池中分配结构：

[**NdisAllocateNetBufferAndNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)

[**NdisAllocateNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)

[**NdisAllocateNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)

调用 **NdisAllocateNetBufferAndNetBufferList** 比调用 **NdisAllocateNetBufferList** 后跟 **NdisAllocateNetBuffer**更有效。 但是， **NdisAllocateNetBufferAndNetBufferList** 只 \_ 在网络 \_ 缓冲区列表结构上创建了一个网络缓冲区结构 \_ 。 若要**使用 NdisAllocateNetBufferAndNetBufferList**，则在调用**NdisAllocateNetBufferListPool**时，驱动程序必须将*AllocateNetBuffer*参数设置为**TRUE** 。

协议驱动程序可以使用 OID 请求来查询底层驱动程序的回退和上下文空间要求。 协议驱动程序应该确定处于 *打开* 或 *重新启动* 状态的绑定的后填充和上下文要求。 驱动程序应为整个堆栈分配足够的后填充和上下文空间。 如有必要，协议驱动程序可以释放池，并在 *重新启动* 状态下重新分配池。

协议驱动程序使用以下功能来释放池：

[**NdisFreeNetBufferListPool**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool)

[**NdisFreeNetBufferPool**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool)。

协议驱动程序使用以下功能来释放从池中分配的结构：

[**NdisFreeNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)

[**NdisFreeNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)

\_在释放关联的**NdisAllocateNetBuffer**网络 \_ 缓冲区列表结构之前，驱动程序应释放用 NdisAllocateNetBuffer 分配的网络缓冲区结构 \_ 。 \_当驱动程序为关联**NdisAllocateNetBufferAndNetBufferList**的**NdisFreeNetBufferList**网络 \_ 缓冲区列表结构调用 NdisFreeNetBufferList 时，将释放用 NdisAllocateNetBufferAndNetBufferList 分配的网络缓冲区结构 \_ 。

 

