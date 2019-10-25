---
title: 无连接低边缘中间驱动程序数据接收
description: 在包含无连接下边缘的中间驱动程序中接收数据
ms.assetid: 73143c2f-4127-41fc-b916-eac87521440a
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 中间驱动程序 WDK，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00cfa34adc8f1f8d724747f069371c3eb6762558
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844850"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connectionless-lower-edge"></a>在包含无连接下边缘的中间驱动程序中接收数据





具有无连接下限的中间驱动程序必须具有[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数才能接收网络数据。

基础无连接微型端口驱动程序调用**NdisMIndicateReceiveNetBufferLists**，并将一个或多个[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的链接列表传递\_列表结构，并将指定结构的所有权放弃为更高级别驱动程序。 当更高级别的驱动程序使用数据时，它们会将 NET\_缓冲区\_列表结构（及其指定资源）返回到微型端口驱动程序。

有关使用无连接的下边缘在中间驱动程序中接收数据的详细信息，请参阅[协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

 

 





