---
title: 面向连接的低边缘中间的驱动程序数据接收
description: 在包含面向连接的下边缘的中间驱动程序中接收数据
ms.assetid: c14b4e8a-cfa2-4771-83b2-aa20fda79d39
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 驱动程序 WDK 的中间，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7cf5b282e06a4c0fb512ff0debc58559f4aeac3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383177"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connection-oriented-lower-edge"></a>在包含面向连接的下边缘的中间驱动程序中接收数据





如果中间驱动程序上的面向连接的微型端口驱动程序进行分层，NDIS 然后调用中间驱动程序[ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)函数来指示接收到的数据。

基础的面向连接的微型端口驱动程序通过调用指示网络数据[ **NdisMCoIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563561)，将一个或多个链接的列表传递[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

有关与面向连接的下边缘中间的驱动程序中接收数据的详细信息，请参阅[Connection-Oriented 操作](connection-oriented-operations.md)。

 

 





