---
title: 克隆的 NET_BUFFER_LIST 结构
description: 克隆的 NET_BUFFER_LIST 结构
ms.assetid: efcf7d03-401e-46da-9ca3-8423af1e385a
keywords:
- NET_BUFFER_LIST
- 克隆的结构 WDK 网络
- 重复结构 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 302d4a906b04bd8340f8a42d400edad5d66c8098
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533359"
---
# <a name="cloned-netbufferlist-structures"></a>克隆 NET\_缓冲区\_列表结构





NDIS 驱动程序创建的克隆[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构从现有的 NET\_缓冲区\_列表结构。 克隆的结构引用的原始结构数据。 驱动程序可以使用此类结构高效地将相同的数据传输到多个路径。

下图显示了父 NET 之间的关系\_缓冲区\_列表结构和克隆的子结构。

![说明 net 父级之间的关系的关系图\-缓冲区\-列表结构和克隆的子结构](images/netbufferlistclone.png)

上图中包含父[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构和派生自该父级的子结构。 父结构有一个[ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构和一个[ **NET\_缓冲区** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) MDLs 附加结构。 父结构的父指针位于**NULL**指示它不派生的结构。

子 NET\_缓冲区\_列表结构有一个 NET\_MDLs 附加缓冲区结构。 子 NET\_缓冲区\_列表具有指向父结构的指针。 **NULL**其中 NET\_缓冲区\_列表\_上下文结构指针会指示子具有任何 NET\_缓冲区\_列表\_上下文结构。

驱动程序调用[ **NdisAllocateCloneNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff560705)函数来创建克隆[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 新分配 NDIS [ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构和以克隆 NET MDLs\_缓冲区\_列表结构。 不会分配 NDIS [ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)克隆结构的结构。 新的 NET\_缓冲区结构和 MDLs 描述与父结构相同的数据。 不复制数据。

驱动程序调用[ **NdisFreeCloneNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff561841)函数来释放 NET\_缓冲区\_列表结构以及所有关联的 NET\_缓冲区结构和 MDL通过调用以前分配的链**NdisAllocateCloneNetBufferList**。

## <a name="related-topics"></a>相关主题


[派生 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






