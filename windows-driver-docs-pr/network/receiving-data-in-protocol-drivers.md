---
title: 在协议驱动程序中接收数据
description: 在协议驱动程序中接收数据
ms.assetid: 758c6a86-6704-410b-ba13-bf589b1e330f
keywords:
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d7f2221106d8118094d6bc05e02d85f47fe7fdf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216956"
---
# <a name="receiving-data-in-protocol-drivers"></a>在协议驱动程序中接收数据





下图说明了一个基本的接收操作，该操作涉及驱动程序堆栈中的协议驱动程序、NDIS 和基础驱动程序。

![说明基本接收操作的关系图，该操作涉及驱动程序堆栈中的协议驱动程序、ndis 和基础驱动程序](images/protocolreceive.png)

NDIS 调用协议驱动程序的 [*ProtocolReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists) 函数来处理来自基础驱动程序的接收指示。 在基础驱动程序调用接收指示函数 (例如， [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)) 指示接收的网络数据或循环回数据后，NDIS 调用*ProtocolReceiveNetBufferLists* 。

如果未设置[*ProtocolReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)的*ReceiveFlags*参数中的**NDIS \_ 接收 \_ 标志 \_ 资源**标志，则在调用[**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数之前，协议驱动程序将保留[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的所有权。 如果 NDIS 设置 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，则协议驱动程序无法保留 **网络 \_ 缓冲区 \_ 列表** 结构和关联的资源。 "设置 **NDIS \_ 接收 \_ 标志 \_ 资源** " 标志指示基础驱动程序在接收资源上运行不足。 在这种情况下， *ProtocolReceiveNetBufferLists* 函数应将接收的数据复制到协议分配的存储中，并尽快返回。

**注意**   NDIS 可以更改基础驱动程序指示的标志。 例如，如果微型端口驱动程序在[**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数的*ReceiveFlags*参数中设置**ndis \_ 接收 \_ 标志 \_ 资源**标志，ndis 可以复制所指示的数据，并将副本传递给[*ProtocolReceiveNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists) ，并清除 " **NDIS \_ 接收 \_ 标志 \_ 资源**" 标志。

 

**注意**   如果设置了**NDIS \_ 接收 \_ 标志 \_ 资源**标志，则协议驱动程序必须在链接列表中保留一组原始的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 例如，当设置此标志时，驱动程序可能会处理这些结构，并一次一个地指示其堆栈，但在函数返回之前，必须还原原始链接列表。

 

协议驱动程序调用 [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists) 函数，以释放 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构列表的所有权以及相关的网络 [** \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构和网络数据。

 

