---
title: 接收网络数据
description: 接收网络数据
ms.assetid: d929c956-73dc-433f-9e60-bc3f8e0bcc14
keywords:
- 网络数据 WDK，接收
- 数据 WDK 网络，接收
- 包 WDK 网络，接收
- 返回数据 WDK 网络
- 网络数据 WDK，返回
- 数据 WDK 网络，返回
- 包 WDK 网络，返回
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3250c3f41e4914a947f3bb7d221b05c15031ce8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844842"
---
# <a name="receiving-network-data"></a>接收网络数据





下图说明了一个基本的接收操作，该操作涉及微型端口驱动程序、NDIS 和协议驱动程序。

![阐释基本接收操作的关系图](images/netbufferreceive.png)

微型端口驱动程序调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数，以便向更高级别的驱动程序指示[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 每个网络\_缓冲结构通常应附加到单独的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 这允许协议驱动程序创建原始列表\_的原始列表的子集\_列表结构，并将其转发到不同的客户端。 某些驱动程序（例如本机 IEEE 802.11 微型端口驱动程序）可能会将多个 NET\_缓冲区结构附加到网络\_缓冲区\_列表结构。

将所有 NET\_缓冲区链接\_列表结构后，微型端口驱动程序会将列表中第一个网络\_\_缓冲区的指针传递到**NdisMIndicateReceiveNetBufferLists**函数。 NDIS 检查 NET\_缓冲区\_列表结构，并调用与 NET\_缓冲区\_列表结构关联的每个协议驱动程序的[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数。 NDIS 传递列表的一个子集，该子集只包含与每个协议驱动程序的正确绑定关联的 NET\_缓冲区\_列表结构。 NDIS 将 NET\_BUFFER\_列表结构中指定的**NetBufferListFrameType**值与每个协议驱动程序注册的帧类型相匹配。

如果 NDIS\_在传递到协议驱动程序的*ProtocolReceiveNetBufferLists*函数的*RECEIVEFLAGS*参数中接收\_标志\_资源标志，Ndis 将重新获得网络的所有权[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) *ProtocolReceiveNetBufferLists*调用返回后，立即缓冲区\_列出结构。

**注意**  如果设置了 NDIS\_接收\_标志\_资源标志，则协议驱动程序必须在链接列表中保留一组原始的 NET\_缓冲区\_列表结构。 例如，当设置此标志时，驱动程序可能会处理这些结构，并一次一个地指示其堆栈，但在函数返回之前，必须还原原始链接列表。

 

如果 NDIS\_接收\_标志，而未设置传递给协议驱动程序的*ProtocolReceiveNetBufferLists*函数的*ReceiveFlags*参数中的资源标志\_资源标志，则协议驱动程序可保留网络的所有权\_缓冲区\_列表结构。 在这种情况下，协议驱动程序必须通过调用[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数来返回 NET\_缓冲区\_列表结构。

如果微型端口驱动程序在接收资源上运行较低，则可以在调用**NdisMIndicateReceiveNetBufferLists**时，在*ReceiveFlags*参数中设置 NDIS\_接收\_标志\_资源标志。 在这种情况下，只要**NdisMIndicateReceiveNetBufferLists**返回，驱动程序就可以回收所有指定的[**net\_缓冲区的所有权\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和嵌入的[**net\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 指示网络\_缓冲区结构与 NDIS\_接收\_标志\_资源标志集强制协议驱动程序复制数据，因此应避免这样做。 微型端口驱动程序应检测即将用完接收资源的时间，并采取必要的步骤来避免这种情况。

在协议驱动程序调用**NdisReturnNetBufferLists**后，NDIS 调用微型端口驱动程序的[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。

**请注意**  如果微型端口驱动程序使用 NDIS\_接收\_标志\_资源标志集来指示网络\_缓冲区\_列表结构，这并不意味着 ndis 将指示 NET\_缓冲区\_列表具有相同状态的协议驱动程序的结构。 例如，NDIS 可以使用 NDIS\_接收\_标志\_资源标志来复制网络\_缓冲区\_列表结构，并指示清除了标志的协议驱动程序的副本。

 

NDIS 可以按任意顺序和任意组合将[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构返回到小型端口驱动程序。 也就是说，通过调用*MiniportReturnNetBufferLists*函数返回给微型端口驱动程序的 NET\_缓冲区\_列表结构的链接列表，可以具有来自不同先前调用的 NET\_缓冲区\_列表结构到**NdisMIndicateReceiveNetBufferLists**。

微型端口驱动程序应将 NET\_缓冲区\_列表结构中的**SourceHandle**成员设置为*MiniportAdapterHandle* ，NDIS 在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数中提供给微型端口驱动程序。 筛选器驱动程序必须将每个 NET\_缓冲区\_列表结构的**SourceHandle**成员设置为该筛选器驱动程序源自[*于该筛选*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)器的**NdisFilterHandle** 。才能. 筛选器驱动程序不能修改任何 NET\_缓冲区中的**SourceHandle**成员\_不受筛选器驱动程序生成的列表结构。

中间驱动程序还将 NET\_BUFFER\_列表结构中的**SourceHandle**成员设置为*MINIPORTADAPTERHANDLE*值，NDIS 在*MiniportInitializeEx*函数中提供给中间驱动程序。 如果中间驱动程序转发接收指示，则驱动程序必须保存基础驱动程序在写入**SourceHandle**成员之前提供的**SourceHandle**值。 当 NDIS 向中间驱动程序返回已转发的 NET\_缓冲区\_列表结构时，中间驱动程序必须还原它保存的**SourceHandle** 。

 

 





