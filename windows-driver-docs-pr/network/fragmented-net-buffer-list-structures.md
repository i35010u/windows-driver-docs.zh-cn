---
title: 分段的 NET_BUFFER_LIST 结构
description: 分段的 NET_BUFFER_LIST 结构
ms.assetid: a72bc0cf-8c92-4c3e-ad10-710e5b93c74c
keywords:
- NET_BUFFER_LIST
- 零碎的结构 WDK 网络
- 将数据结构分为 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3fbd576c43675f9c04d2191b2858dae451fb698
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839646"
---
# <a name="fragmented-net_buffer_list-structures"></a>零碎的 NET\_缓冲区\_列表结构





NDIS 驱动程序可以通过现有的 NET\_缓冲区\_列表结构从现有的 NET [ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 零碎结构引用一组引用原始数据的[**NET\_缓冲器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构;但是，数据被划分为不超过最大大小的单位。 驱动程序可以使用这种类型的结构将大型缓冲区有效地分解为较小的缓冲区。

下图显示了 parent\_缓冲区\_列表结构与零碎子级之间的关系。

![说明 parent\-缓冲区\-列表结构和碎片子结构之间的关系的关系图](images/netbufferlistfragment.png)

上图包含一个父[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和派生自该父对象的子结构。 父结构具有一个[**网络\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构和一个连接了 MDLs 的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 父结构的父指针为**NULL** ，表示它不是派生的结构。

子网\_缓冲区\_列表结构具有三个附加了 MDLs 的网络\_缓冲区结构。 子网\_缓冲区\_列表结构具有指向父结构的指针。 如果**为 NULL** ，则 NET\_缓冲区\_列表\_上下文结构指针将指示子网中没有 NET\_缓冲区\_列表\_的上下文结构。

NDIS 驱动程序调用[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)函数来创建新的零散[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，该结构基于现有 NET\_缓冲区\_列表结构中的数据。 NDIS 为分段网络\_缓冲区\_列表结构分配新的[**net\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构和 MDLs。 NDIS 不会为分段结构[ **\_列表\_上下文结构分配 NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)。 片段 NET\_BUFFER 结构和 MDLs 描述与父结构相同的数据。 不会复制数据。

**NdisAllocateFragmentNetBufferList**创建片段，从每个父网络中所*用数据空间*的开头开始\_BUFFER 结构，并按*StartOffset*参数中指定的值进行偏移。

[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)将每个源网络\_缓冲区结构中的已*用数据空间*划分为片段。 每个片段的所*用数据空间*的长度小于或等于*MaximumLength*参数中指定的值。 最后一个片段的已*用数据空间*可以小于*MaximumLength* 。 新的 NET\_缓冲区结构的数据偏移量 retreated 在*DataOffsetDelta*参数中指定的字节数。

如果父[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中有多个[**net\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构\_列表结构（图中未显示），则每个 net\_缓冲区结构的分段过程与单个构造. 例如，如果任何 parent NET\_缓冲区结构中的最后一个数据块小于最大大小，NDIS 不会将此类数据与下一 NET\_缓冲区结构开头的数据进行合并。

NDIS 驱动程序调用[**NdisFreeFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreefragmentnetbufferlist)函数\_以\_列表结构和所有关联的 NET\_缓冲结构和 MDL 链（以前通过调用[**NdisAllocateFragmentNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)。

## <a name="related-topics"></a>相关主题


[派生的 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






