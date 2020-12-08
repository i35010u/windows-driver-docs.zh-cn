---
title: 分段的 NET_BUFFER_LIST 结构
description: 分段的 NET_BUFFER_LIST 结构
keywords:
- NET_BUFFER_LIST
- 零碎的结构 WDK 网络
- 将数据结构分为 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7be56097a92470d94171da2dcce2438f360a3e50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825519"
---
# <a name="fragmented-net_buffer_list-structures"></a>碎片网络 \_ 缓冲区 \_ 列表结构





NDIS 驱动程序可以从现有的网络缓冲区列表结构创建分段 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构 \_ \_ 。 零碎结构引用一组引用原始数据的 [**网络 \_ 缓冲**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构，但数据被划分为不超过最大大小的单位。 驱动程序可以使用这种类型的结构将大型缓冲区有效地分解为较小的缓冲区。

下图显示了父网络 \_ 缓冲区 \_ 列表结构与零碎子级之间的关系。

![说明父网络 \- 缓冲区 \- 列表结构与零碎子结构之间的关系的关系图](images/netbufferlistfragment.png)

上图包含一个父 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构和一个派生自该父级的子结构。 父结构具有一个 [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构和一个附加了 MDLs 的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构。 父结构的父指针为 **NULL** ，表示它不是派生的结构。

子网络 \_ 缓冲区 \_ 列表结构具有三个 \_ 附加了 MDLs 的网络缓冲区结构。 子网络 \_ 缓冲区 \_ 列表结构具有指向父结构的指针。 如果 **NULL** 网络 \_ 缓冲区 \_ 列表 \_ 上下文指针为 NULL，则表示子级没有网络 \_ 缓冲区 \_ 列表 \_ 上下文结构。

NDIS 驱动程序调用 [**NdisAllocateFragmentNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist) 函数来创建新的零散 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构，该结构基于现有网络 \_ 缓冲区列表结构中的数据 \_ 。 NDIS 为分段网络缓冲区列表结构分配新的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构和 MDLs \_ \_ 。 对于零碎结构，NDIS 不分配 [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构。 片段网络 \_ 缓冲区结构和 MDLs 描述的数据与父结构相同。 不会复制数据。

**NdisAllocateFragmentNetBufferList** 创建片段，从每个父网络缓冲区结构中所 *用数据空间* 的开头开始， \_ 按 *StartOffset* 参数中指定的值进行偏移。

[**NdisAllocateFragmentNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist) 将每个源网络缓冲区结构中的已 *用数据空间* 划分 \_ 为片段。 每个片段的所 *用数据空间* 的长度小于或等于 *MaximumLength* 参数中指定的值。 最后一个片段的已 *用数据空间* 可以小于 *MaximumLength* 。 新的网络缓冲区结构的数据偏移量 \_ 将 retreated 在 *DataOffsetDelta* 参数中指定的字节数。

如果父 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中存在多个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构 (图中未显示) 则每个网络缓冲区结构的分段过程与 \_ 单个结构相同。 例如，如果任何父网络缓冲区结构中的最后一个数据块小于 \_ 最大大小，NDIS 不会将此类数据与下一网络缓冲区结构开头的数据进行合并 \_ 。

NDIS 驱动程序调用 [**NdisFreeFragmentNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreefragmentnetbufferlist) 函数，以释放网络 \_ 缓冲区 \_ 列表结构以及所有关联的网络 \_ 缓冲区结构和 MDL 链，这些链以前通过调用 [**NdisAllocateFragmentNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatefragmentnetbufferlist)分配。

## <a name="related-topics"></a>相关主题


[派生的网络 \_ 缓冲区 \_ 列表结构](derived-net-buffer-list-structures.md)

 

