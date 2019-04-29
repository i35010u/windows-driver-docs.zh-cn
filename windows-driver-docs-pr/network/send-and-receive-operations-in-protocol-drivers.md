---
title: 协议驱动程序中的发送和接收操作
description: 协议驱动程序中的发送和接收操作
ms.assetid: 4759725b-ed0b-4345-9cdc-9411ee29ebdb
keywords:
- 协议驱动程序 WDK 网络，接收操作
- NDIS 协议驱动程序 WDK，接收操作
- 协议驱动程序 WDK 网络发送操作
- NDIS 协议驱动程序 WDK，发送操作
- 发送操作 WDK NDIS 协议
- 接收操作 WDK NDIS 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 388e2e6910487cbf05a992a2a35584c901352048
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368243"
---
# <a name="send-and-receive-operations-in-protocol-drivers"></a>协议驱动程序中的发送和接收操作





有两个不同接口发送和接收协议的 NDIS 驱动程序中的操作。 协议具有较低的无连接边缘调用的驱动程序[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)函数来发送网络数据。 无连接协议驱动程序必须提供[ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)函数。 NDIS 调用*ProtocolReceiveNetBufferLists*当基础的无连接的微型端口驱动程序调用[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数指示接收的网络数据。 有关发送和接收无连接协议驱动程序中的数据的详细信息，请参阅[协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

面向连接的 NDIS (CoNDIS) 协议驱动程序调用[ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)函数来发送网络数据。 CoNDIS 协议驱动程序必须提供[ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)函数。 NDIS 调用*ProtocolCoReceiveNetBufferLists*当基础的 CoNDIS 微型端口驱动程序调用[ **NdisMCoIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563561)函数来指示接收的网络数据。 有关发送和面向连接的协议驱动程序中的操作的详细信息，请参阅[Connection-Oriented 操作](connection-oriented-operations.md)。

若要发送和接收操作的说明，请参阅[发送和接收操作](send-and-receive-operations.md)。

 

 





