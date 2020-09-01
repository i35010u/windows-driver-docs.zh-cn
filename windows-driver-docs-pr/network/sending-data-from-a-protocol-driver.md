---
title: 从协议驱动程序发送数据
description: 从协议驱动程序发送数据
ms.assetid: f4fa1814-1d8f-49d3-90fb-766b5b17ef28
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ba2abfc1f2a1f9ae81151a5a2313c77790fb23
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208579"
---
# <a name="sending-data-from-a-protocol-driver"></a>从协议驱动程序发送数据





下图说明了一个协议驱动程序发送操作，该操作涉及驱动程序堆栈中的协议驱动程序、NDIS 和基础驱动程序。

![阐释协议驱动程序发送操作的关系图，该操作涉及驱动程序堆栈中的协议驱动程序、ndis 和基础驱动程序](images/protocolsend.png)

协议驱动程序调用 [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists) 函数来发送网络 [** \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构列表中定义的网络数据。

协议驱动程序必须将每个网络缓冲区列表结构的 **SourceHandle** 成员设置 \_ \_ 为其传递给 *NdisBindingHandle* 参数的相同值。 在 \_ \_ 基础微型端口驱动程序调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)后，绑定句柄提供 NDIS 要求将网络缓冲区列表结构返回到协议驱动程序的信息。

在调用 **NdisSendNetBufferLists**之前，协议驱动程序可以使用 [**网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_info) 宏设置发送请求附带的信息。 底层驱动程序可以通过 NET \_ BUFFER \_ 列表信息宏检索此信息 \_ 。

一旦协议驱动程序调用 **NdisSendNetBufferLists**，它就会让给网络 \_ 缓冲区 \_ 列表结构和所有关联资源的所有权。 NDIS 调用 [**ProtocolSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete) 函数将结构和数据返回到协议驱动程序。 在将 \_ \_ 列表传递到 *PROTOCOLSENDNETBUFFERLISTSCOMPLETE*之前，NDIS 可以将多个发送请求中的结构和数据收集到网络缓冲区列表结构的单个链接列表中。

在 NDIS 调用 *ProtocolSendNetBufferListsComplete*之前，协议驱动程序启动的发送的当前状态是未知的。 协议驱动程序会在调用 **NdisSendNetBufferLists**时暂时释放它为发送请求分配的所有资源的所有权。 在 NDIS 将结构返回到 ProtocolSendNetBufferListsComplete 之前，协议驱动程序绝不应尝试检查网络 \_ 缓冲区 \_ 列表结构或任何关联*ProtocolSendNetBufferListsComplete*的数据。

*ProtocolSendNetBufferListsComplete* 执行完成发送操作所需的任何后处理操作。 例如，协议驱动程序可以通知客户端，请求发送网络数据的协议驱动程序，发送操作已完成。

当 NDIS 调用 *ProtocolSendNetBufferListsComplete*时，协议驱动程序会重新获得与 \_ \_ *NetBufferLists* 参数指定的网络缓冲区列表结构关联的所有资源的所有权。 *ProtocolSendNetBufferListsComplete*可以通过调用 NdisFreeNetBuffer 和 NdisFreeNetBufferList 来释放这些资源 (例如，通过调用[**NdisFreeNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)和[**NdisFreeNetBufferList**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbufferlist)) 或准备在对**NdisSendNetBufferLists**的后续调用中重复使用。

尽管 NDIS 始终将协议提供的网络数据以协议确定的顺序提交给 **NdisSendNetBufferLists**，但基础驱动程序可以按随机顺序完成发送请求。 也就是说，每个绑定协议驱动程序都可以依赖 NDIS 将协议驱动程序传递到 **NdisSendNetBufferLists** 的网络数据提交到底层驱动程序。 但是，任何协议驱动程序都不能依赖于基础驱动程序以相同顺序调用 **NdisMSendNetBufferListsComplete** 。

 

