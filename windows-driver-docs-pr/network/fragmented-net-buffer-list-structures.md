---
title: 分段的 NET_BUFFER_LIST 结构
description: 分段的 NET_BUFFER_LIST 结构
ms.assetid: a72bc0cf-8c92-4c3e-ad10-710e5b93c74c
keywords:
- NET_BUFFER_LIST
- 碎片化的结构 WDK 网络
- 将数据结构 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a3ae0737449e89f582b33bd74d589ce8bc84c4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323472"
---
# <a name="fragmented-netbufferlist-structures"></a>分段 NET\_缓冲区\_列表结构





NDIS 驱动程序可以创建零碎[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构从现有的 NET\_缓冲区\_列表结构。 碎片化的结构引用的一组[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构的引用的原始数据; 但是，将数据划分成不能超过最大大小的单位。 驱动程序可以使用这种类型的结构来有效地分解成较小的缓冲区的大型缓冲区。

下图显示了父 NET 之间的关系\_缓冲区\_列表结构且是零碎的子级。

![说明 net 父级之间的关系的关系图\-缓冲区\-列表结构和碎片化的子结构](images/netbufferlistfragment.png)

上图中包含父[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构和派生自该父级的子结构。 父结构有一个[ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构和一个[ **NET\_缓冲区** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) MDLs 附加结构。 父结构的父指针位于**NULL**指示它不派生的结构。

子 NET\_缓冲区\_列表结构具有三个 NET\_具有 MDLs 附加缓冲区结构。 子 NET\_缓冲区\_列表结构具有指向父结构的指针。 **NULL**其中 NET\_缓冲区\_列表\_上下文结构指针会指示子具有任何 NET\_缓冲区\_列表\_上下文结构。

NDIS 驱动程序调用[ **NdisAllocateFragmentNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff560707)函数来创建一个新分片[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)基于现有网络中的数据结构\_缓冲区\_列表结构。 新分配 NDIS [ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构和 MDLs 有关分片的 NET\_缓冲区\_列表结构。 不会分配 NDIS [ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)碎片化结构的结构。 片段 NET\_缓冲区结构和 MDLs 描述相同的数据与父结构。 不复制数据。

**NdisAllocateFragmentNetBufferList**创建从开头开始的片段*用数据空间*中每个父 NET\_缓冲区结构和通过中指定的值的偏移量*StartOffset*参数。

[**NdisAllocateFragmentNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff560707)划分*用数据空间*中每个源 NET\_缓冲区为片段的结构。 长度*已用数据空间*的每个片段是小于或等于中指定的值*MaximumLength*参数。 *已用数据空间*的最后一个片段可以小于*MaximumLength* 。 新的 NET 的数据偏移量\_缓冲区结构 retreated 中指定的字节数*DataOffsetDelta*参数。

如果有多个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构的父代中[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388) （不在图中所示） 结构每个网络的 fragmenting 过程\_缓冲区结构与单个结构相同。 例如，如果任何中的数据最后一条父 NET\_缓冲区结构小于最大大小、 NDIS 不能合并此类数据与开头的下一步的 NET 数据\_缓冲区结构。

NDIS 驱动程序调用[ **NdisFreeFragmentNetBufferList** ](https://msdn.microsoft.com/library/windows/hardware/ff561847)函数来释放 NET\_缓冲区\_列表结构以及所有关联的 NET\_缓冲区结构和以前分配的调用的 MDL 链[ **NdisAllocateFragmentNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff560707)。

## <a name="related-topics"></a>相关主题


[派生 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






