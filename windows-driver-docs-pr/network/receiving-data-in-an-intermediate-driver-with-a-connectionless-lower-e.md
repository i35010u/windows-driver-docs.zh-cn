---
title: 无连接较低的边缘中间的驱动程序数据接收
description: 在包含无连接下边缘的中间驱动程序中接收数据
ms.assetid: 73143c2f-4127-41fc-b916-eac87521440a
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 驱动程序 WDK 的中间，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3010f683cb8233295e500ed564b2c1d1d6f458cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383175"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connectionless-lower-edge"></a>在包含无连接下边缘的中间驱动程序中接收数据





使用无连接的下边缘中间驱动程序必须具有[ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)函数来接收网络数据。

基础无连接的微型端口驱动程序调用**NdisMIndicateReceiveNetBufferLists**，传递的一个或多个链接的列表[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构，来重新释放到更高级别驱动程序的指定结构的所有权。 当较高级别驱动程序已用完数据时，它们返回 NET\_缓冲区\_微型端口驱动程序列表结构 （或指定的资源）。

有关使用无连接的下边缘中间的驱动程序中接收数据的详细信息，请参阅[协议驱动程序发送和接收操作](protocol-driver-send-and-receive-operations.md)。

 

 





