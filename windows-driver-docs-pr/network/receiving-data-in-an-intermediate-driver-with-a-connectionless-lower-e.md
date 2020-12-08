---
title: 无连接低边缘中间驱动程序数据接收
description: 在包含无连接下边缘的中间驱动程序中接收数据
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 中间驱动程序 WDK，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d91356c75c4f0a999654fb505102e71e111872bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792127"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connectionless-lower-edge"></a>在包含无连接下边缘的中间驱动程序中接收数据





具有无连接下限的中间驱动程序必须具有 [**ProtocolReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists) 函数才能接收网络数据。

基础无连接微型端口驱动程序调用 **NdisMIndicateReceiveNetBufferLists**，将一个或多个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的链接列表传递到更高级别的驱动程序，将所指示的结构的所有权放弃。 当更高级别的驱动程序使用数据时，它们会将网络 \_ 缓冲区 \_ 列表结构返回 (和它们指定的资源) 到微型端口驱动程序。

有关使用无连接的下边缘在中间驱动程序中接收数据的详细信息，请参阅 [协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

 

