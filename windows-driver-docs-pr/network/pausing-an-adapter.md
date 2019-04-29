---
title: 暂停适配器
description: 暂停适配器
ms.assetid: e24a9886-a1d7-4ca5-bed8-85db4a49ed9c
keywords:
- 微型端口适配器 WDK 连接网络、 暂停
- 适配器 WDK 连接网络、 暂停
- 正在暂停状态 WDK 网络
- 暂停的状态 WDK 网络
- MiniportPause
- 正在暂停微型端口适配器
- 正在停止微型端口适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4316b3e0eaaeaa7dca4c9b8552b1dec49d519556
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385013"
---
# <a name="pausing-an-adapter"></a>暂停适配器





NDIS 调用微型端口驱动程序[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)函数以启动暂停操作。 暂停操作完成之前，适配器将仍处于暂停状态。

在暂停状态下，微型端口驱动程序必须完成未完成接收操作。 该驱动程序还必须完成任何未完成发送操作，它应拒绝任何新的发送请求。

若要完成接收操作，该驱动程序等待所有调用的[ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)函数以返回 NDIS 必须返回所有未完成[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)微型端口驱动程序的结构[ *MiniportReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559437)函数。

若要完成未完成发送操作，微型端口驱动程序应调用[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数的所有未完成的 NET\_缓冲区\_列表结构。 该驱动程序应拒绝对任何新的发送请求其[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)立即函数。

微型端口驱动程序完成所有未完成发送和接收操作后，该驱动程序必须同步或异步完成暂停请求。 如果以异步方式完成暂停操作，则该驱动程序调用[ **NdisMPauseComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563628)完成暂停请求。 完成后暂停请求，微型端口驱动程序处于已暂停状态。

NDIS 并不会启动其他插操作、 暂停工作，如初始化、 电源更改，或重新启动操作，微型端口驱动程序处于暂停状态时。 NDIS 可以启动这些插操作后的微型端口驱动程序处于已暂停状态。

 

 





