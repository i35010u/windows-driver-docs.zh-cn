---
title: 接收网络数据
description: 接收网络数据
ms.assetid: d929c956-73dc-433f-9e60-bc3f8e0bcc14
keywords:
- 网络数据 WDK，接收
- WDK 数据网络、 接收
- 数据包 WDK 网络、 接收
- 返回数据 WDK 网络
- 网络数据 WDK，返回
- 返回的数据 WDK 网络
- 返回的数据包 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a7861e971f5bfff28c3002a1c6dcf66ef959ce5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385430"
---
# <a name="receiving-network-data"></a>接收网络数据





下图说明了基本的接收操作，这涉及到微型端口驱动程序、 NDIS 和协议驱动程序。

![说明一个简单的关系图的接收操作](images/netbufferreceive.png)

微型端口驱动程序调用[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数来指示[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)更高级别驱动程序的结构。 每个 NET\_缓冲区结构通常应附加到一个单独[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 这允许协议驱动程序创建的 NET 的原始列表的子集\_缓冲区\_列表结构并将其转发到不同的客户端。 某些驱动程序，例如本机 IEEE 802.11 微型端口驱动程序，可以附加多个 NET\_缓冲区结构 NET\_缓冲区\_列表结构。

在链接所有 NET 后\_缓冲区\_列表结构，则微型端口驱动程序会将指针传递到第一个 NET\_缓冲区\_到列表中的列表结构**NdisMIndicateReceiveNetBufferLists**函数。 NDIS 检查 NET\_缓冲区\_列表结构和它调用[ **ProtocolReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数的每个与网络相关联的协议驱动程序\_缓冲区\_列表结构。 NDIS 传递的列表，包括仅 NET 子集\_缓冲区\_与正确的绑定到每个协议驱动程序相关联的列表结构。 NDIS 匹配**NetBufferListFrameType** NET 中指定的值\_缓冲区\_列表结构与每个协议驱动程序注册的框架类型。

如果 NDIS\_接收\_标志\_中的资源标记*ReceiveFlags*传递到协议驱动程序的参数*ProtocolReceiveNetBufferLists*函数设置、 NDIS 重新获得的所有权[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构后立即*ProtocolReceiveNetBufferLists*调用返回。

**请注意**  如果 NDIS\_接收\_标志\_资源标志设置，则协议驱动程序必须保留原始的一组 NET\_缓冲区\_中链接的列表结构列表。 例如，设置此标志驱动程序可能处理结构并指示它们其中一个在堆栈中向上一次，但之前该函数将返回它，必须还原原始链接的列表。

 

如果 NDIS\_接收\_标志\_中的资源标记*ReceiveFlags*传递到协议驱动程序的参数*ProtocolReceiveNetBufferLists*未设置函数，协议驱动程序可以保留所有权的 NET\_缓冲区\_列表结构。 在这种情况下，协议驱动程序必须返回 NET\_缓冲区\_通过调用列表结构[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)函数。

如果正在低微型端口驱动程序在接收资源，但它可以设置 NDIS\_接收\_标志\_中的资源标记*ReceiveFlags*参数对的调用中**NdisMIndicateReceiveNetBufferLists**。 在这种情况下，该驱动程序可以回收所有的所有权所指示[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构和嵌入[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构一旦**NdisMIndicateReceiveNetBufferLists**返回。 指示 NET\_缓冲区结构与的 NDIS\_接收\_标志\_资源标志设置强制协议驱动程序以将数据复制，因此应当避免。 微型端口驱动程序应检测它即将运行时接收资源并执行任何步骤，所需避免这种情况。

NDIS 调用微型端口驱动程序[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)函数之后，协议驱动程序调用**NdisReturnNetBufferLists**。

**请注意**  如果微型端口驱动程序指示 NET\_缓冲区\_NDIS 列表结构\_接收\_标志\_资源标志设置，并不意味着 NDIS 将指示 NET\_缓冲区\_列表结构具有相同状态的协议驱动程序。 例如，可以将 NDIS 复制 NET\_缓冲区\_列表结构与的 NDIS\_接收\_标志\_资源标志设置和清除的标志指示复制到协议驱动程序。

 

可以返回 NDIS [ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)微型端口驱动程序和任何组合中任何任意顺序的结构。 即，链接的列表的 NET\_缓冲区\_列表结构返回的回微型端口驱动程序通过调用其*MiniportReturnNetBufferLists*函数中，可以有 NET\_缓冲区\_从对不同的上一个调用列表结构**NdisMIndicateReceiveNetBufferLists**。

微型端口驱动程序应设置**SourceHandle**成员在 NET\_缓冲区\_列表结构到*MiniportAdapterHandle*到中的微型端口驱动程序提供该 NDIS[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 必须设置筛选器驱动程序**SourceHandle**的每个 NET 成员\_缓冲区\_到筛选器的筛选器驱动程序产生的列表结构**NdisFilterHandle**该 NDIS提供给中的筛选器驱动程序[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数。 筛选器驱动程序不能修改**SourceHandle**成员中任何 NET\_缓冲区\_不由筛选器驱动程序产生的列表结构。

中间驱动程序还设置**SourceHandle**成员在 NET\_缓冲区\_列表结构*MiniportAdapterHandle*值提供给中间的 NDIS中的驱动程序*MiniportInitializeEx*函数。 如果中间驱动程序将转发的接收指示，该驱动程序必须将保存**SourceHandle**基础驱动程序，提供之前它将写入到的值**SourceHandle**成员。 当 NDIS 返回转发的 NET\_缓冲区\_必须还原到中间驱动程序，中间驱动程序的列表结构**SourceHandle**保存它。

 

 





