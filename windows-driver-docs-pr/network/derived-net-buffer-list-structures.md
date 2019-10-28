---
title: 派生的 NET_BUFFER_LIST 结构
description: 派生的 NET_BUFFER_LIST 结构
ms.assetid: 6660aef5-ba67-4f15-98b6-547fa753bc76
keywords:
- NET_BUFFER_LIST
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
- 包 WDK 网络，数据结构
- 派生结构 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d970c35850e435335985f00b722b8af2650b072
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838158"
---
# <a name="derived-net_buffer_list-structures"></a>派生的 NET\_缓冲区\_列表结构





NDIS 提供了一些函数，驱动程序可以使用这些函数来管理从其他 NET\_缓冲区\_列表结构派生的[**net\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 这些函数通常由中间驱动程序使用。

以下 NDIS 函数可以从现有 NET\_缓冲区\_列表结构创建派生的 NET\_缓冲区\_列表结构：

[**NdisAllocateCloneNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateclonenetbufferlist)

[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)

[**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)

这些函数会提高系统性能，因为 NDIS 在不复制网络数据的情况下创建派生的结构。 有三种类型的[**net\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，可以从现有的 NET\_缓冲区\_列表结构派生：

<a href="" id="clone"></a>克隆  
克隆的 NET\_缓冲区\_列表结构是一个引用原始数据的重复。 驱动程序可以使用这种类型的结构有效地将相同的数据传输到多个路径。

<a href="" id="fragment"></a>代码  
分段[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构包含一组引用原始数据的[**NET\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构;但是，数据被划分为不超过最大大小的单位。 驱动程序可以使用这种类型的结构将大型缓冲区有效地分解为较小的缓冲区。

<a href="" id="reassembled"></a>目的地  
重新组合的 NET\_缓冲区\_列表结构包含一个 NET\_缓冲结构，该结构引用多个源网络\_缓冲区结构中的原始数据。 驱动程序可以使用这种类型的结构将很多较小的缓冲区有效地合并为一个大的缓冲区。

以下主题提供有关派生的 NET\_缓冲区\_列表结构的详细信息：

-   [NET\_BUFFER\_列表生成之间的关系](relationships-between-net-buffer-list-generations.md)
-   [克隆的 NET\_缓冲区\_列表结构](cloned-net-buffer-list-structures.md)
-   [零碎的 NET\_缓冲区\_列表结构](fragmented-net-buffer-list-structures.md)
-   [重新组合网络\_缓冲区\_列表结构](reassembled-net-buffer-list-structures.md)

 

 





