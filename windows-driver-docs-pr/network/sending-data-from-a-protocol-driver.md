---
title: 从协议驱动程序发送数据
description: 从协议驱动程序发送数据
ms.assetid: f4fa1814-1d8f-49d3-90fb-766b5b17ef28
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d62a59ae9aec083551fd4783a8b0d40f223790f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841975"
---
# <a name="sending-data-from-a-protocol-driver"></a>从协议驱动程序发送数据





下图说明了一个协议驱动程序发送操作，该操作涉及驱动程序堆栈中的协议驱动程序、NDIS 和基础驱动程序。

![阐释协议驱动程序发送操作的关系图，该操作涉及驱动程序堆栈中的协议驱动程序、ndis 和基础驱动程序](images/protocolsend.png)

协议驱动程序调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数来发送网络\_缓冲区列表中定义的网络数据[ **\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

协议驱动程序必须将每个 NET\_缓冲区\_列表结构的**SourceHandle**成员设置为传递给*NdisBindingHandle*参数的相同值。 在基础微型端口驱动程序调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)后，绑定句柄提供 NDIS 要求将 NET\_\_缓冲区返回到协议驱动程序的信息。

在调用**NdisSendNetBufferLists**之前，协议驱动程序可以使用[**NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏设置发送请求附带的信息。 底层驱动程序可以通过 NET\_缓冲区\_列表\_信息宏检索此信息。

一旦协议驱动程序调用**NdisSendNetBufferLists**，它就让给了 NET\_缓冲区的所有权\_列表结构和所有关联的资源。 NDIS 调用[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)函数将结构和数据返回到协议驱动程序。 在将列表传递到*ProtocolSendNetBufferListsComplete*之前，NDIS 可以将多个发送请求中的结构和数据收集到网络\_缓冲区的单个链接列表中\_列表结构。

在 NDIS 调用*ProtocolSendNetBufferListsComplete*之前，协议驱动程序启动的发送的当前状态是未知的。 协议驱动程序会在调用**NdisSendNetBufferLists**时暂时释放它为发送请求分配的所有资源的所有权。 在 NDIS 将结构返回到*ProtocolSendNetBufferListsComplete*之前，协议驱动程序决不会尝试检查 NET\_缓冲区\_列表结构或任何关联的数据。

*ProtocolSendNetBufferListsComplete*执行完成发送操作所需的任何后处理操作。 例如，协议驱动程序可以通知客户端，请求发送网络数据的协议驱动程序，发送操作已完成。

当 NDIS 调用*ProtocolSendNetBufferListsComplete*时，协议驱动程序会重新获得*NetBufferLists*参数指定的与 NET\_\_缓冲区关联的所有资源的所有权。 *ProtocolSendNetBufferListsComplete*可以释放这些资源（例如，通过调用[**NdisFreeNetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)和[**NdisFreeNetBufferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)），或准备好它们以便在对**NdisSendNetBufferLists**的后续调用中重复使用。

尽管 NDIS 始终将协议提供的网络数据以协议确定的顺序提交给**NdisSendNetBufferLists**，但基础驱动程序可以按随机顺序完成发送请求。 也就是说，每个绑定协议驱动程序都可以依赖 NDIS 将协议驱动程序传递到**NdisSendNetBufferLists**的网络数据提交到底层驱动程序。 但是，任何协议驱动程序都不能依赖于基础驱动程序以相同顺序调用**NdisMSendNetBufferListsComplete** 。

 

 





