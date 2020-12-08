---
title: 面向连接的下边缘中间驱动程序数据接收
description: 在包含面向连接的下边缘的中间驱动程序中接收数据
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 中间驱动程序 WDK，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40d07364425653c1ab4a0f6f56cfcd153c57d0e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805157"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connection-oriented-lower-edge"></a>在包含面向连接的下边缘的中间驱动程序中接收数据





如果中间驱动程序在面向连接的微型端口驱动程序之上，NDIS 会调用中间驱动程序的 [**ProtocolCoReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists) 函数来指示收到的数据。

面向连接的基础微型端口驱动程序通过调用 [**NdisMCoIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)来指示网络数据，并传递一个或多个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的链接列表。

有关使用面向连接的下边缘在中间驱动程序中接收数据的详细信息，请参阅 [面向连接的操作](connection-oriented-operations-performed-by-clients.md)。

 

