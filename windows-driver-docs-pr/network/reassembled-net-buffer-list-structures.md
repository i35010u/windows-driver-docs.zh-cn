---
title: 重新汇编的 NET_BUFFER_LIST 结构
description: 重新汇编的 NET_BUFFER_LIST 结构
ms.assetid: 0bfbfef3-c3ac-4add-b3b8-a4c3a96c8baa
keywords:
- NET_BUFFER_LIST
- 重新组合的结构 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 037763cf9e1de621b14a2a122692be441e3aa268
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323570"
---
# <a name="reassembled-netbufferlist-structures"></a>重新组合 NET\_缓冲区\_列表结构





NDIS 驱动程序可以创建重新组合[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构从现有的 NET\_缓冲区\_列表结构。 重新组合的结构引用的原始数据从多个源[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。 驱动程序可以使用这种类型的结构，有效地将许多较小的缓冲区合并到单个大型缓冲区。

下图显示了父 NET 之间的关系\_缓冲区\_列表结构和重新组合的子结构：

![说明 net 父级之间的关系的关系图\-缓冲区\-列表结构和重新组合的子结构 ](images/netbufferlistreassembled.png)

上图中包含父[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构和派生自该父级的子结构。 父结构有一个[ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构和第三个[ **NET\_缓冲区** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)具有 MDLs 附加的结构。 父结构的父指针位于**NULL**指示它不派生的结构。

子 NET\_缓冲区\_列表结构有一个 NET\_MDLs 附加缓冲区结构。 子 NET\_缓冲区\_列表结构具有指向父结构的指针。 **NULL**其中 NET\_缓冲区\_列表\_上下文结构指针会指示子具有任何 NET\_缓冲区\_列表\_上下文结构。

NDIS 驱动程序调用[ **NdisAllocateReassembledNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff561614)函数以重新组装零碎[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 分配一个新的 NDIS [ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构和以重新组合的 NET MDLs\_缓冲区\_列表结构。 NDIS 不会分配 NET\_缓冲区\_列表\_重新组合结构的上下文结构。 重新组合的 NET\_缓冲区结构和 MDLs 描述相同的数据与父结构。 不复制数据。

若要创建重新组合的 NET\_缓冲区\_列表结构**NdisAllocateReassembledNetBufferList**跳过中指定的字节数目*StartOffset*参数在每个父 NET\_缓冲区结构。 **NdisAllocateReassembledNetBufferList**串联剩余数据的每个父 NET\_到一个重新组合 NET MDL 链的缓冲区结构\_缓冲区结构。 **NdisAllocateReassembledNetBufferList**整顿 （增加使用的数据空间中） 重新组合的 NET\_缓冲区中指定的数量的结构*DataOffsetDelta* 。

NDIS 驱动程序调用[ **NdisFreeReassembledNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff562594)函数来释放重新组合[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构和关联[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构和 MDL 链。

## <a name="related-topics"></a>相关主题


[派生 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






