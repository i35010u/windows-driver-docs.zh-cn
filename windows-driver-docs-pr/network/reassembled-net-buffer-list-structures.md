---
title: 重新汇编的 NET_BUFFER_LIST 结构
description: 重新汇编的 NET_BUFFER_LIST 结构
ms.assetid: 0bfbfef3-c3ac-4add-b3b8-a4c3a96c8baa
keywords:
- NET_BUFFER_LIST
- 重新组合结构 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f186db1cde6f7a0f5135071489f0435de4e73cd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208597"
---
# <a name="reassembled-net_buffer_list-structures"></a>重新组合网络 \_ 缓冲区 \_ 列表结构





NDIS 驱动程序可以从现有的网络缓冲区列表结构创建重新组合的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构 \_ \_ 。 重新组合结构引用多个源 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构中的原始数据。 驱动程序可以使用这种类型的结构将很多较小的缓冲区有效地合并为一个大的缓冲区。

下图显示了父网络 \_ 缓冲区 \_ 列表结构和重新组合子结构之间的关系：

![说明父网络 \- 缓冲区 \- 列表结构和重新组合子结构之间的关系的关系图 ](images/netbufferlistreassembled.png)

上图包含一个父 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构和一个派生自该父级的子结构。 父结构具有一个 [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context) 结构和三个附加了 MDLs 的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构。 父结构的父指针为 **NULL** ，表示它不是派生的结构。

子网络 \_ 缓冲区 \_ 列表结构具有一个 \_ 附加了 MDLs 的网络缓冲区结构。 子网络 \_ 缓冲区 \_ 列表结构具有指向父结构的指针。 如果**NULL**网络 \_ 缓冲区 \_ 列表 \_ 上下文指针为 NULL，则表示子级没有网络 \_ 缓冲区 \_ 列表 \_ 上下文结构。

NDIS 驱动程序调用 [**NdisAllocateReassembledNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist) 函数来重新组装分段 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。 NDIS 使用重新组合的网络缓冲区列表结构分配新的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构和 MDLs \_ \_ 。 对于重新组合结构，NDIS 不分配网络 \_ 缓冲区 \_ 列表 \_ 上下文结构。 重新组合的网络 \_ 缓冲区结构和 MDLs 描述的数据与父结构相同。 不会复制数据。

若要创建重新组合的网络 \_ 缓冲区 \_ 列表结构， **NdisAllocateReassembledNetBufferList** 将跳过每个父网络缓冲区结构中 *StartOffset* 参数中指定的字节数 \_ 。 **NdisAllocateReassembledNetBufferList** 将每个父网络缓冲区结构中的剩余数据连接 \_ 到一个重新组合网络缓冲区结构的 MDL 链 \_ 。 **NdisAllocateReassembledNetBufferList** 退出 (\_ 按照 *DataOffsetDelta* 中指定的数量增加了重新组合后的网络缓冲区) 中的已用数据空间。

NDIS 驱动程序调用 [**NdisFreeReassembledNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreereassemblednetbufferlist) 函数以释放重新组合的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构和关联的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构和 MDL 链。

## <a name="related-topics"></a>相关主题


[派生的网络 \_ 缓冲区 \_ 列表结构](derived-net-buffer-list-structures.md)

 

