---
title: 协议驱动程序中的发送和接收操作
description: 协议驱动程序中的发送和接收操作
ms.assetid: 4759725b-ed0b-4345-9cdc-9411ee29ebdb
keywords:
- 协议驱动程序 WDK 网络，接收操作
- NDIS 协议驱动程序 WDK，接收操作
- 协议驱动程序 WDK 网络，发送操作
- NDIS 协议驱动程序 WDK，发送操作
- 发送操作 WDK NDIS 协议
- 接收操作 WDK NDIS 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b02fab051dc6d3c7b1b50a84bff672b54924c52
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841987"
---
# <a name="send-and-receive-operations-in-protocol-drivers"></a>协议驱动程序中的发送和接收操作





在 NDIS 协议驱动程序中，发送和接收操作有两个不同的接口。 具有无连接下限的协议驱动程序调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数来发送网络数据。 无连接协议驱动程序必须提供[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数。 当基础无连接微型端口驱动程序调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数以指示接收的网络数据时，NDIS 将调用*ProtocolReceiveNetBufferLists* 。 有关在无连接协议驱动程序中发送和接收数据的详细信息，请参阅[协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

面向连接的 NDIS （CoNDIS）协议驱动程序调用[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)函数来发送网络数据。 CoNDIS 协议驱动程序必须提供[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)函数。 当基础 CoNDIS 微型端口驱动程序调用[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)函数以指示接收的网络数据时，NDIS 将调用*ProtocolCoReceiveNetBufferLists* 。 有关面向连接的协议驱动程序中的发送和操作的详细信息，请参阅[面向连接的操作](connection-oriented-operations.md)。

有关发送和接收操作的简介，请参阅[发送和接收操作](send-and-receive-operations.md)。

 

 





