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
ms.openlocfilehash: df57023a8360c92dab68a8e99fa78783477cfdaa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844864"
---
# <a name="reassembled-net_buffer_list-structures"></a>重新组合网络\_缓冲区\_列表结构





NDIS 驱动程序可以通过现有 NET\_缓冲区\_列表结构，创建一个重新组合的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 重新组合结构引用多个源[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构中的原始数据。 驱动程序可以使用这种类型的结构将很多较小的缓冲区有效地合并为一个大的缓冲区。

下图显示了 parent\_缓冲区\_列表结构和重新组合子结构之间的关系：

![说明 parent\-缓冲区\-列表结构和重新组合子结构之间的关系的关系图 ](images/netbufferlistreassembled.png)

上图包含一个父[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和派生自该父对象的子结构。 父结构具有一个[**网络\_缓冲区\_列表\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list_context)结构和三个[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构（附加了 MDLs）。 父结构的父指针为**NULL** ，表示它不是派生的结构。

子网\_缓冲区\_列表结构具有一个附加了 MDLs 的 NET\_缓冲区结构。 子网\_缓冲区\_列表结构具有指向父结构的指针。 如果**为 NULL** ，则 NET\_缓冲区\_列表\_上下文结构指针将指示子网中没有 NET\_缓冲区\_列表\_的上下文结构。

NDIS 驱动程序调用[**NdisAllocateReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatereassemblednetbufferlist)函数来重新组合[ **\_缓冲器\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 NDIS 使用重新组合的网络\_缓冲区\_列表结构分配新的[**net\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构和 MDLs。 NDIS 不会为重新组合结构\_列表\_上下文结构分配 NET\_缓冲区。 重新组合的 NET\_BUFFER 结构和 MDLs 描述与父结构相同的数据。 不会复制数据。

若要创建重新组合的 NET\_缓冲区\_列表结构， **NdisAllocateReassembledNetBufferList**会跳过每个 parent NET\_缓冲区结构中*指定的字节*数。 **NdisAllocateReassembledNetBufferList**将每个 parent NET\_缓冲区结构中的剩余数据连接到一个重新组合的网络\_缓冲区结构的 MDL 链中。 **NdisAllocateReassembledNetBufferList**退出（增加中的已用数据空间），重新组合后的网络\_缓冲结构按*DataOffsetDelta*中指定的数量。

NDIS 驱动程序调用[**NdisFreeReassembledNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreereassemblednetbufferlist)函数以释放重新组合的[**net\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和关联的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构和 MDL 链。

## <a name="related-topics"></a>相关主题


[派生的 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






