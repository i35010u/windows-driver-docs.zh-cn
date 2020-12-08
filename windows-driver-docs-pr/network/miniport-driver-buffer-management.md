---
title: 微型端口驱动程序缓冲区管理
description: 微型端口驱动程序缓冲区管理
keywords:
- 缓冲 WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 046d92d03813bfb641ee802d541f476b1a65d535
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802325"
---
# <a name="miniport-driver-buffer-management"></a>微型端口驱动程序缓冲区管理





微型端口驱动程序通常从 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)调用 [**NdisAllocateNetBufferListPool**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool) ，以创建 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的池。 微型端口驱动程序使用这些结构指示接收的数据。

通常，分配网络缓冲区列表结构的微型端口驱动程序 \_ \_ 将在该网络缓冲区列表结构上分配一个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构并对其进行排队 \_ \_ 。 \_当分配网络缓冲区列表结构的池而不是 \_ \_ 单独分配网络 \_ 缓冲区 \_ 列表结构和网络 \_ 缓冲区结构时，可以更有效地预分配网络缓冲区结构。

微型端口驱动程序可以调用 **NdisAllocateNetBufferListPool** ，并将 *AllocateNetBuffer* 参数设置为 **TRUE** ，以指示已预分配 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构。 在这种情况下，将 \_ 使用 \_ \_ 驱动程序从池中分配的每个网络缓冲区列表结构预分配网络缓冲区结构。 此类驱动程序必须调用 [**NdisAllocateNetBufferAndNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist) ，才能从此池分配结构。

通常情况下，微型端口驱动程序从 *MiniportInitializeEx* 调用 **NdisAllocateNetBufferAndNetBufferList** ，以便分配尽可能多的缓冲区，因为后续接收操作将需要该缓冲区。 在这种情况下，驱动程序管理可用缓冲区的内部列表。

[*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数可准备返回的网络 \_ 缓冲区 \_ 列表结构，以便在后续接收指示中重复使用。 尽管 *MiniportReturnNetBufferLists* 可以将网络 \_ 缓冲区 \_ 列表结构返回到池 (例如，它可以) 调用 [**NdisFreeNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist) ，因此在不将其返回到池的情况下重用结构会更有效。

当 NDIS 停止适配器时，微型端口驱动程序应释放所有网络 \_ 缓冲区 \_ 列表结构和关联的数据。 驱动程序可以调用 **NdisFreeNetBufferList** 来释放结构，使用 [**NDISFREENETBUFFERLISTPOOL**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool) 函数释放网络 \_ 缓冲区 \_ 列表池。

 

