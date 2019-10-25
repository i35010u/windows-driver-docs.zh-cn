---
title: 协议驱动程序缓冲区管理
description: 协议驱动程序缓冲区管理
ms.assetid: 1f91b58e-d432-46c8-994e-d95c3aadfe43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9beede3d57e6f9ef741e036e0b3b7c6bc53c6f6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844916"
---
# <a name="protocol-driver-buffer-management"></a>协议驱动程序缓冲区管理





协议驱动程序必须为发送操作管理[**net\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构池和[**net\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)池。 若要创建这些池，驱动程序将调用以下函数：

[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool)

[**NdisAllocateNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferpool)

协议驱动程序可以使用以下函数从池中分配结构：

[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)

[**NdisAllocateNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlist)

[**NdisAllocateNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)

调用**NdisAllocateNetBufferAndNetBufferList**比调用**NdisAllocateNetBufferList**后跟**NdisAllocateNetBuffer**更有效。 但是， **NdisAllocateNetBufferAndNetBufferList**仅在网络\_缓冲区\_列表结构上创建了一个网络\_缓冲区结构。 若要**使用 NdisAllocateNetBufferAndNetBufferList**，则在调用**NdisAllocateNetBufferListPool**时，驱动程序必须将*AllocateNetBuffer*参数设置为**TRUE** 。

协议驱动程序可以使用 OID 请求来查询底层驱动程序的回退和上下文空间要求。 协议驱动程序应该确定处于*打开*或*重新启动*状态的绑定的后填充和上下文要求。 驱动程序应为整个堆栈分配足够的后填充和上下文空间。 如有必要，协议驱动程序可以释放池，并在*重新启动*状态下重新分配池。

协议驱动程序使用以下功能来释放池：

[**NdisFreeNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool)

[**NdisFreeNetBufferPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferpool)。

协议驱动程序使用以下功能来释放从池中分配的结构：

[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)

[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)

在释放关联的网络\_缓冲区\_列表结构之前，驱动程序应释放用**NdisAllocateNetBuffer**分配的 NET\_缓冲区结构。 当驱动程序为关联的网络\_缓冲区\_列表结构调用**NdisFreeNetBufferList**时，将释放用**NDISALLOCATENETBUFFERANDNETBUFFERLIST**分配的 net\_缓冲区结构。

 

 





