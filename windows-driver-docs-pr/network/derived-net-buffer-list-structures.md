---
title: 派生的 NET_BUFFER_LIST 结构
description: 派生的 NET_BUFFER_LIST 结构
ms.assetid: 6660aef5-ba67-4f15-98b6-547fa753bc76
keywords:
- NET_BUFFER_LIST
- 网络数据 WDK，结构
- 数据 WDK 网络结构
- 数据包 WDK 网络、 数据结构
- 派生的结构 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 410a584a46ac704fe6cd43c8ed7ccfc26417e689
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381457"
---
# <a name="derived-netbufferlist-structures"></a>派生 NET\_缓冲区\_列表结构





NDIS 提供了可用于管理驱动程序的函数[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构派生自其他 NET\_缓冲区\_列表结构。 通过中间驱动程序通常使用这些函数。

以下的 NDIS 函数可以创建派生的 NET\_缓冲区\_从现有的 NET 列表结构\_缓冲区\_列表结构：

[**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocateclonenetbufferlist)

[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)

[**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)

这些函数提高系统性能，因为 NDIS 创建派生的结构而不复制的网络数据。 有三种类型的[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构可以派生自现有 NET\_缓冲区\_列表结构：

<a href="" id="clone"></a>克隆  
一个克隆 NET\_缓冲区\_列表结构是重复的引用的原始数据。 驱动程序可以使用此类结构高效地将相同的数据传输到多个路径。

<a href="" id="fragment"></a>片段  
片段[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构包括一组[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)引用的原始数据; 的结构但是，将数据分为不能超过最大大小的单位。 驱动程序可以使用这种类型的结构来有效地分解成较小的缓冲区的大型缓冲区。

<a href="" id="reassembled"></a>重新组合  
重新组合的 NET\_缓冲区\_列表结构包含 NET\_从多个源 NET 引用原始数据的缓冲区结构\_缓冲区结构。 驱动程序可以使用这种类型的结构，有效地将许多较小的缓冲区合并到单个大型缓冲区。

此以下主题提供有关派生 NET 的详细信息\_缓冲区\_列表结构：

-   [NET 之间的关系\_缓冲区\_列表代](relationships-between-net-buffer-list-generations.md)
-   [克隆 NET\_缓冲区\_列表结构](cloned-net-buffer-list-structures.md)
-   [分段 NET\_缓冲区\_列表结构](fragmented-net-buffer-list-structures.md)
-   [重新组合 NET\_缓冲区\_列表结构](reassembled-net-buffer-list-structures.md)

 

 





