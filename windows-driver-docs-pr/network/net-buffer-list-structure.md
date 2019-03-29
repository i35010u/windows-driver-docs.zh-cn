---
title: NET_BUFFER_LIST 结构
description: NET_BUFFER_LIST 结构
ms.assetid: f7f19e48-cb63-458d-b175-6f99080e4cdf
keywords:
- NET_BUFFER_LIST
- 网络数据 WDK，结构
- 数据 WDK 网络结构
- 数据包 WDK 网络、 数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce60b4adcbb38b5090190385a7cc03b711bbf5cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575165"
---
# <a name="netbufferlist-structure"></a>NET\_缓冲区\_列表结构





一个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构包 NET 的链接的列表\_缓冲区结构。

下图显示字段在 NET\_缓冲区\_列表结构。

![说明在网络中的字段的关系图\-缓冲区\-列表结构](images/netbufferlist.png)

NET\_缓冲区\_列表结构包括[ **NET\_缓冲区\_列表\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff568400)结构**NetBufferListHeader**成员。 NET\_缓冲区\_列表\_标头结构包括[ **NET\_缓冲区\_列表\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568393)结构**NetBufferListData**成员。 应使用 NDIS 宏来访问 NET\_缓冲区\_列表结构成员。 有关这些宏的详细信息，请参阅[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构参考页。

某些成员仅供 NDIS。 以下列表中定义的驱动程序很可能会使用的成员：

<a href="" id="parentnetbufferlist"></a>**ParentNetBufferList**  
如果 NET\_缓冲区\_列表结构是从父项 （克隆、 碎片，或重组），派生的子级**ParentNetBufferList**指定指向父 NET\_缓冲区\_列表结构。 否则，此参数是**NULL**。

<a href="" id="ndispoolhandle"></a>**NdisPoolHandle**  
指定标识的池句\_缓冲区\_从该列表池 NET\_缓冲区\_列表结构已分配。

<a href="" id="protocolreserved"></a>**ProtocolReserved**  
保留供协议驱动程序。

<a href="" id="miniportreserved"></a>**MiniportReserved**  
保留供微型端口驱动程序。

<a href="" id="sourcehandle"></a>**SourceHandle**  
NDIS 向绑定或通过使用以下驱动程序所提供的例程的一个附加操作中的驱动程序提供一个句柄：

<a href="" id="miniport-driver"></a>微型端口驱动程序  
[*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)

<a href="" id="protocol-driver"></a>协议驱动程序  
[*ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)

<a href="" id="filter-driver"></a>筛选器驱动程序  
[*FilterAttach*](https://msdn.microsoft.com/library/windows/hardware/ff549905)

使用 NDIS **SourceHandle**返回 NET\_缓冲区\_驱动程序的发送 NET 列表结构\_缓冲区\_列表结构。 NDIS 驱动程序不应读取此句柄。

<a href="" id="childrefcount"></a>**ChildRefCount**  
如果[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构是 （具有通过克隆、 片段或重装配操作派生的子级） 的父级， **ChildRefCount**指定的现有子级的个数。 否则，此参数为零。

<a href="" id="flags"></a>**标志**  
保留供将来规范的属性 NET\_缓冲区\_列表结构。 当前没有任何标志可用于驱动程序。

<a href="" id="status"></a>**状态**  
指定此网络的网络数据操作的最终的完成状态\_缓冲区\_列表结构。 微型端口驱动程序完成发送操作之前写入此值。

<a href="" id="netbufferlistinfo"></a>**NetBufferListInfo**  
指定[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构信息普遍适用于所有[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)列表中的结构。 此信息通常称为"带外 (OOB) 数据。"

<a href="" id="next"></a>**下一步**  
指定指向下一步 NET\_缓冲区\_NET 链接列表中的列表结构\_缓冲区\_列表结构。 如果 NET\_缓冲区\_列表结构是在列表中的最后一个结构，此成员是**NULL**。

<a href="" id="firstnetbuffer"></a>**FirstNetBuffer**  
指定指向第一个 NET\_NET 的链接列表中的缓冲区结构\_与此网络相关联的缓冲区结构\_缓冲区\_列表结构。

**请注意**  **上下文**指向的指针[ **NET\_缓冲区\_列表\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff568389)结构。 宏和函数来操作上的数据，提供了 NDIS**上下文**。 详细了解 NET\_缓冲区\_列表\_上下文结构，请参阅[NET\_缓冲区\_列表\_上下文结构](net-buffer-list-context-structure.md)。

 

 

 





