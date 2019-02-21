---
title: NET_BUFFER 结构
description: NET_BUFFER 结构
ms.assetid: 6ba44aef-d4e6-4f18-8ae3-aebd8045791f
keywords:
- NET_BUFFER
- 网络数据 WDK，结构
- 数据 WDK 网络结构
- 数据包 WDK 网络、 数据结构
- NDIS_PACKET
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2339a151b20ca6196d0b669b69ae63b37ddea0f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544564"
---
# <a name="netbuffer-structure"></a>NET\_缓冲区结构





NDIS 6.0 及更高版本[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构是类似于[ **NDIS\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff557086)使用 NDIS 5 的结构。*x*和早期驱动程序。 每个网络\_缓冲区结构包的网络数据包。

下图显示在网络中的字段\_缓冲区结构。

![说明在网络中的字段的关系图\-缓冲结构](images/netbuffer.png)

NET\_缓冲区结构包括[ **NET\_缓冲区\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff568387)结构**NetBufferHeader**成员。 NET\_缓冲区\_标头结构包括[ **NET\_缓冲区\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568381)结构**NetBufferData**成员。 应使用 NDIS 宏来访问 NET\_缓冲区结构成员。 有关这些宏的完整列表，请参阅[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构参考页。

一些[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构成员仅供 NDIS。 驱动程序通常使用的成员包括：

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
保留供协议驱动程序。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
保留供微型端口驱动程序。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
指定标识的池句\_从其缓冲池 NET\_缓冲区结构已分配。

<a href="" id="next"></a>**下一步**  
指定指向下一步 NET\_NET 的链接列表中的缓冲区结构\_缓冲区结构。 如果这是最后一个 NET\_缓冲区结构在列表中，此成员是**NULL**。

<a href="" id="datalength"></a>**DataLength**  
指定的长度以字节为单位的 MDL 链中的网络数据。

<a href="" id="dataoffset"></a>**DataOffset**  
指定偏移量，以字节为单位，从开始到 MDL 链中的网络数据的起始位置 MDL 链中的内存。

<a href="" id="currentmdl"></a>**CurrentMdl**  
指定指向当前驱动程序使用的第一个 MDL 的指针。 此指针提供了一种优化，它通过跳过当前驱动程序不使用任何 MDLs 提高性能。

<a href="" id="currentmdloffset"></a>**CurrentMdlOffset**  
指定的偏移量，以字节为单位，到使用的数据空间中指定的 MDL 的开头**CurrentMdl** NET 成员\_缓冲区结构。

下图显示了之间的关系**CurrentMdl**， **CurrentMdlOffset**， **DataOffset**，以及**DataLength**成员和数据空间。

![说明数据空间分配的关系图](images/netbufferdata-wmdl.png)

NDIS 提供了用于管理 MDL 链中的数据空间的函数。 使用当前驱动程序动态更改驱动程序如何使用数据空间。 有时是由当前驱动程序当前未使用的数据空间。 尽管*未使用的数据空间*当前未使用，它可以包含有效的数据。 例如，在接收路径上*未使用的数据空间*可以包含已由较低级别的驱动程序的标头信息。

驱动程序执行撤回，促进操作来增加和减少*已用数据空间*。 有关参加和高级操作的详细信息，请参阅[撤回和高级操作](retreat-and-advance-operations.md)。

以下术语和定义描述的元素[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)数据空间：

<a href="" id="used-data-space"></a>使用的数据空间  
*已用数据空间*包含当前驱动程序使用的当前时间的数据。 驱动程序提高*已用数据空间*与参加操作并减少*用数据空间*与高级操作。

<a href="" id="unused-data-space"></a>未使用的数据空间  
当前驱动程序在当前时间不使用此数据空间。

<a href="" id="total-data-size"></a>总数据大小  
总数据大小是大小的总和*已用数据空间*并*未使用的数据空间*。 若要计算的总大小，请添加**DataOffset**到**DataLength** 。

<a href="" id="retreat"></a>参加  
参加操作增加的大小*已用数据空间*。

<a href="" id="advance"></a>高级  
高级操作减小的大小*已用数据空间*。

 

 





