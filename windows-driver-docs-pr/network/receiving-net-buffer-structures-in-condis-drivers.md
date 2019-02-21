---
title: 接收 NET_BUFFER 结构中的 CoNDIS 驱动程序
description: 接收 NET_BUFFER 结构中的 CoNDIS 驱动程序
ms.assetid: b3bbd3ef-9206-4edc-8f7a-4ce896d77150
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e923133330db0932a3c0656c6607736e8e575df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534480"
---
# <a name="receiving-netbuffer-structures-in-condis-drivers"></a>接收 NET\_缓冲区中的 CoNDIS 驱动程序的结构





下图说明了基本的 CoNDIS 接收操作，这涉及到协议驱动程序、 NDIS 和微型端口驱动程序。

![说明基本 condis 的关系图的接收操作，这涉及到协议驱动程序、 ndis 和微型端口驱动程序](images/netbuffercoreceive.png)

如前图所示，微型端口驱动程序调用[ **NdisMCoIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563561)函数来指示[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)到过量驱动程序的结构。 在大多数的微型端口驱动程序中每个 NET\_缓冲区结构附加到一个单独[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，因此协议驱动程序可以创建子集NET 的原始列表的\_缓冲区\_列表结构并将其转发到不同的客户端。 但是，NET 数\_缓冲区结构附加到 NET\_缓冲区\_列表取决于驱动程序。

后微型端口驱动程序链接所有 NET\_缓冲区\_列表结构，则微型端口驱动程序会将指针传递到第一个 NET\_缓冲区\_到列表中的列表结构**NdisMCoIndicateReceiveNetBufferLists**函数。 NDIS 检查 NET\_缓冲区\_列表结构并调用[ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)与关联的协议驱动程序的函数指定的虚拟连接 (VC)。 NDIS 传递的列表，包括仅 NET 子集\_缓冲区\_与正确的绑定到每个协议驱动程序相关联的列表结构。

如果 NDIS\_接收\_标志\_状态\_中设置资源标志*CoReceiveFlags*协议驱动程序的参数*ProtocolCoReceiveNetBufferLists*函数，NDIS 重新获得所有权[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)后立即结构*ProtocolCoReceiveNetBufferLists*返回。

如果 NDIS\_接收\_标志\_状态\_未设置资源标志*CoReceiveFlags*协议驱动程序的参数[ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)函数，协议驱动程序可以保留的 NET 所有权\_缓冲区\_列表结构。 在这种情况下，协议驱动程序必须返回 NET\_缓冲区\_通过调用列表结构[ **NdisReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564534)函数。

如果运行在较低的微型端口驱动程序在接收资源，但它可以设置 NDIS\_接收\_标志\_状态\_中的资源标记*CoReceiveFlags*参数[ **NdisMCoIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563561)函数。 在这种情况下，该驱动程序可以回收所有所指示的所有权[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构和嵌入[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构一旦**NdisMCoIndicateReceiveNetBufferLists**返回。 如果微型端口驱动程序指示 NET\_缓冲区结构与的 NDIS\_接收\_标志\_资源标志设置，协议驱动程序必须复制数据，因此，应避免使用 NDIS\_接收\_标志\_这种方式中的资源。 具有低接收资源和应完成所需避免这种情况的任何步骤时，应检测到的微型端口驱动程序。

NDIS 调用微型端口驱动程序[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)函数之后，协议驱动程序调用**NdisReturnNetBufferLists**。

**请注意**  如果微型端口驱动程序指示[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)给定状态、 NDIS 结构不需要它来指示 NET\_缓冲区\_列表结构具有相同状态的基础驱动程序。 例如，可以将 NDIS 复制 NET\_缓冲区\_列表结构与的 NDIS\_接收\_标志\_资源标志设置和清除此标志指示复制到基础驱动程序。

 

NDIS 可以返回 NET\_缓冲区\_微型端口驱动程序和任何组合中任何任意顺序列表结构。 即，链接的列表的 NET\_缓冲区\_NDIS 通过调用返回至微型端口驱动程序的列表结构[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)可以具有 NET\_缓冲区\_从对不同的上一个调用列表结构[ **NdisMCoIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563561)。

微型端口驱动程序必须设置**SourceHandle**中的成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构为相同的值为*NdisVcHandle*的参数**NdisMCoIndicateReceiveNetBufferLists**。 以便 NDIS 可以返回 NET\_缓冲区\_到正确的微型端口驱动程序的列表结构。

中间驱动程序还设置**SourceHandle**成员在 NET\_缓冲区\_列表结构*NdisVcHandle*值。 如果中间驱动程序将转发的接收指示，该驱动程序必须将保存**SourceHandle**基础驱动程序，提供之前它将写入到的值**SourceHandle**成员。 当 NDIS 返回转发的 NET\_缓冲区\_必须还原到中间驱动程序，中间驱动程序的列表结构**SourceHandle**保存它。

 

 





