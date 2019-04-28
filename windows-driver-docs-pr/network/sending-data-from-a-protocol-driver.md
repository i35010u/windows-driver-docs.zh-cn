---
title: 从协议驱动程序发送数据
description: 从协议驱动程序发送数据
ms.assetid: f4fa1814-1d8f-49d3-90fb-766b5b17ef28
keywords:
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32850e4e9c84895cd6c4de4661003ff275596c6a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346783"
---
# <a name="sending-data-from-a-protocol-driver"></a>从协议驱动程序发送数据





下图说明了涉及协议驱动程序、 NDIS 驱动程序堆栈中的基础驱动程序和协议驱动程序发送操作。

![说明协议驱动程序的关系图发送操作，这涉及到协议驱动程序、 ndis 和驱动程序堆栈中的基础驱动程序](images/protocolsend.png)

协议驱动程序调用[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)函数来发送的列表中定义的网络数据[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

协议驱动程序必须设置**SourceHandle**的每个 NET 成员\_缓冲区\_将其传递到的相同值的列表结构*NdisBindingHandle*参数。 绑定句柄介绍 NDIS 需要返回 NET\_缓冲区\_给基础的微型端口驱动程序调用后协议驱动程序的列表结构[ **NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668)。

然后再调用**NdisSendNetBufferLists**，协议驱动程序可以设置发送请求，附带的信息[ **NET\_缓冲区\_列表\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff568401)宏。 基础驱动程序可以检索此信息与 NET\_缓冲区\_列表\_信息宏。

只要协议驱动程序调用**NdisSendNetBufferLists**，它将放弃所有权的 NET\_缓冲区\_列表结构和所有关联的资源。 NDIS 调用[ **ProtocolSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570268)函数以返回到协议驱动程序的结构和数据。 NDIS 可以收集结构和数据从多个将请求发送到一个链接列表的 NET\_缓冲区\_列表结构传递到列表之前*ProtocolSendNetBufferListsComplete*。

NDIS 调用直到*ProtocolSendNetBufferListsComplete*，协议驱动程序启动发送的当前状态为未知。 协议驱动程序暂时释放它分配给发送请求时，它调用的所有资源的所有权**NdisSendNetBufferLists**。 协议驱动程序应永远不会尝试检查 NET\_缓冲区\_列表结构或任何关联数据，然后 NDIS 返回到结构再*ProtocolSendNetBufferListsComplete*。

*ProtocolSendNetBufferListsComplete*执行任何后续处理是完成发送操作所必需。 例如，协议驱动程序可以通知客户端，请求协议驱动程序，以发送网络数据，发送操作已完成。

当调用 NDIS *ProtocolSendNetBufferListsComplete*，协议驱动程序重新获得所有与网络相关联的资源的所有权\_缓冲区\_由指定的列表结构*NetBufferLists*参数。 *ProtocolSendNetBufferListsComplete*可以是释放这些资源 (例如，通过调用[ **NdisFreeNetBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff562582)并[ **NdisFreeNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff562583)) 或让其可供在后续调用中重用**NdisSendNetBufferLists**。

尽管 NDIS 始终提交到基础的微型端口驱动程序的顺序确定协议的协议提供网络数据传递给**NdisSendNetBufferLists**，基础驱动程序，可以完成中随机的发送请求顺序。 也就是说，每个绑定的协议驱动程序可以依赖提交协议驱动程序将传递到的网络数据的 NDIS **NdisSendNetBufferLists**到基础驱动程序的先进先出顺序。 但是，没有协议驱动程序可以依赖于基础驱动程序来调用**NdisMSendNetBufferListsComplete**顺序相同。

 

 





