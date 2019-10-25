---
title: 微型端口驱动程序缓冲区管理
description: 微型端口驱动程序缓冲区管理
ms.assetid: 3b8844e0-9b38-4030-9aec-b713643de523
keywords:
- 缓冲 WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec22e69bb4b068aba0959651d54a80a67626bc81
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844240"
---
# <a name="miniport-driver-buffer-management"></a>微型端口驱动程序缓冲区管理





微型端口驱动程序通常从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)调用[**NdisAllocateNetBufferListPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferlistpool) ，以创建[ **\_缓冲区池\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 微型端口驱动程序使用这些结构指示接收的数据。

通常情况下，分配网络\_缓冲区\_列表结构的微型端口驱动程序将在该网络\_缓冲区\_列表结构上分配一个[**网络\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构并对该结构进行排队。 当分配网络\_缓冲区池\_列表结构的池，而不是分别分配网络\_缓冲区\_列表结构和 NET\_缓冲结构时，预分配 NET\_缓冲区结构的效率更高。

微型端口驱动程序可以调用**NdisAllocateNetBufferListPool** ，并将*AllocateNetBuffer*参数设置为**TRUE** ，以指示[**网络\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构已预分配。 在这种情况下，将使用驱动程序从池中分配的每个网络\_缓冲区\_列表结构预分配网络\_缓冲区结构。 此类驱动程序必须调用[**NdisAllocateNetBufferAndNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist) ，才能从此池分配结构。

通常情况下，微型端口驱动程序从*MiniportInitializeEx*调用**NdisAllocateNetBufferAndNetBufferList** ，以便分配尽可能多的缓冲区，因为后续接收操作将需要该缓冲区。 在这种情况下，驱动程序管理可用缓冲区的内部列表。

[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数可准备返回的 NET\_缓冲区\_列表结构，以便在后续接收指示中重复使用。 尽管*MiniportReturnNetBufferLists*可以将 NET\_BUFFER\_列表结构返回到池（例如，它可以调用[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)），但如果不将这些结构返回到，则可以更高效地重用它们。池。

当 NDIS 停止适配器时，微型端口驱动程序应释放所有 NET\_缓冲区\_列表结构和关联数据。 驱动程序可以调用**NdisFreeNetBufferList**来释放结构，使用[**NDISFREENETBUFFERLISTPOOL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlistpool)函数释放 NET\_缓冲区\_列表池。

 

 





