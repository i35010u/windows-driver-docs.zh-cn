---
title: 协议驱动程序缓冲区管理
description: 协议驱动程序缓冲区管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f6d3808336e9ca77e331d9a477cba9d9feefb17
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247908"
---
# <a name="protocol-driver-buffer-management"></a>协议驱动程序缓冲区管理





协议驱动程序必须管理 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构池和 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构池，以便发送操作。 若要创建这些池，驱动程序将调用以下函数：

[**NdisAllocateNetBufferListPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferlistpool)

[**NdisAllocateNetBufferPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferpool)

协议驱动程序可以使用以下函数从池中分配结构：

[**NdisAllocateNetBufferAndNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferandnetbufferlist)

[**NdisAllocateNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbufferlist)

[**NdisAllocateNetBuffer**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatenetbuffer)

调用 **NdisAllocateNetBufferAndNetBufferList** 比调用 **NdisAllocateNetBufferList** 后跟 **NdisAllocateNetBuffer** 更有效。 但是， **NdisAllocateNetBufferAndNetBufferList** 只 \_ 在网络 \_ 缓冲区列表结构上创建了一个网络缓冲区结构 \_ 。 若要 **使用 NdisAllocateNetBufferAndNetBufferList**，则在调用 **NdisAllocateNetBufferListPool** 时，驱动程序必须将 *AllocateNetBuffer* 参数设置为 **TRUE** 。

协议驱动程序可以使用 OID 请求来查询底层驱动程序的回退和上下文空间要求。 协议驱动程序应该确定处于 *打开* 或 *重新启动* 状态的绑定的后填充和上下文要求。 驱动程序应为整个堆栈分配足够的后填充和上下文空间。 如有必要，协议驱动程序可以释放池，并在 *重新启动* 状态下重新分配池。

协议驱动程序使用以下功能来释放池：

[**NdisFreeNetBufferListPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbufferlistpool)

[**NdisFreeNetBufferPool**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbufferpool)。

协议驱动程序使用以下功能来释放从池中分配的结构：

[**NdisFreeNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbufferlist)

[**NdisFreeNetBuffer**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreenetbuffer)

\_在释放关联的网络 \_ 缓冲区列表结构之前，驱动程序应释放用 NdisAllocateNetBuffer 分配的网络缓冲区结构 \_ 。 \_当驱动程序为关联的网络 \_ 缓冲区列表结构调用 NdisFreeNetBufferList 时，将释放用 NdisAllocateNetBufferAndNetBufferList 分配的网络缓冲区结构 \_ 。

 

