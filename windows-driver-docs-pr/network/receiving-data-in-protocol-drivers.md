---
title: 在协议驱动程序中接收数据
description: 在协议驱动程序中接收数据
ms.assetid: 758c6a86-6704-410b-ba13-bf589b1e330f
keywords:
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42267f671d4cd1f33eaad7a0eaed962c670d4cb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843470"
---
# <a name="receiving-data-in-protocol-drivers"></a>在协议驱动程序中接收数据





下图说明了一个基本的接收操作，该操作涉及驱动程序堆栈中的协议驱动程序、NDIS 和基础驱动程序。

![说明基本接收操作的关系图，该操作涉及驱动程序堆栈中的协议驱动程序、ndis 和基础驱动程序](images/protocolreceive.png)

NDIS 调用协议驱动程序的[*ProtocolReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数来处理来自基础驱动程序的接收指示。 在基础驱动程序调用接收指示函数（例如， [**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)）后，NDIS 调用*ProtocolReceiveNetBufferLists*来指示接收的网络数据或循环回数据。

如果 NDIS\_在[*ProtocolReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)的*RECEIVEFLAGS*参数中**接收\_标志\_资源**标志，则协议驱动程序将保留[**NET\_缓冲区的所有权\_列出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，直到它调用[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数。 如果 NDIS 将**ndis\_接收\_标志\_资源**标志，则协议驱动程序无法保留**NET\_缓冲区\_列表**结构和关联的资源。 Set **NDIS\_接收\_标志\_资源**标志表明底层驱动程序在接收资源上运行不足。 在这种情况下， *ProtocolReceiveNetBufferLists*函数应将接收的数据复制到协议分配的存储中，并尽快返回。

**请注意**  NDIS 可以更改基础驱动程序指示的标志。 例如，如果微型端口驱动程序设置 NDIS\_在[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数的*RECEIVEFLAGS*参数中**接收\_标志\_资源**标志，则 NDIS 可以复制所指示的数据并将副本传递给[*ProtocolReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists) ，并将**NDIS\_接收\_标志\_资源**标志已清除。

 

**注意**  如果设置了**NDIS\_接收\_标志\_资源**标志，则协议驱动程序必须在链接列表中保留一组原始的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 例如，当设置此标志时，驱动程序可能会处理这些结构，并一次一个地指示其堆栈，但在函数返回之前，必须还原原始链接列表。

 

协议驱动程序调用[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数，以释放[**net\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的列表的所有权以及相关的[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构和网络数据。

 

 





