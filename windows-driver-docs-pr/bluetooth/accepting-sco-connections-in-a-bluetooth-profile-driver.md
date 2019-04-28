---
title: 在蓝牙配置文件驱动程序中接受 SCO 连接
description: 在蓝牙配置文件驱动程序中接受 SCO 连接
ms.assetid: 9736f113-26fb-4e2f-9a58-9874a11f8347
keywords:
- 同步面向连接的 WDK 蓝牙
- SCO 配置文件驱动程序 WDK 蓝牙
- 传入的 SCO 连接请求 WDK 蓝牙
- 远程连接通知 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8637ca3f86556e94a1cc8b047abc01fdc9e5f925
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328344"
---
# <a name="accepting-sco-connections-in-a-bluetooth-profile-driver"></a>在蓝牙配置文件驱动程序中接受 SCO 连接


SCO 配置文件驱动程序可以将其以响应传入 Synchronous Connection-Oriented (SCO) 连接请求从远程设备进行注册。 例如，无绳电话服务配置文件 (CTP) 设备的 SCO 配置文件驱动程序与传入 SCO 连接请求响应来自 CTP 设备，接受或拒绝请求。 如果服务器配置文件驱动程序接受该请求，服务器配置文件驱动程序将响应输入设备，然后将该输入对于蓝牙驱动程序堆栈。

服务器配置文件驱动程序必须执行以下步骤以接受传入 SCO 连接请求从远程蓝牙设备。

**若要接收传入 SCO 连接请求从远程设备**

1.  配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_SCO\_注册\_服务器**](https://msdn.microsoft.com/library/windows/hardware/ff536628)请求以便注册[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)与蓝牙驱动程序堆栈以便堆栈可以通知传入 SCO 连接请求的配置文件驱动程序。

2.  当蓝牙驱动程序堆栈从远程设备收到传入 SCO 连接请求时，它将调用[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)以前注册配置文件驱动程序。 将值传递的蓝牙驱动程序堆栈**ScoIndicationRemoteConnect**到*指示*回调函数的参数。

3.  若要对传入连接请求做出响应，配置文件驱动程序应生成并发送[ **BRB\_SCO\_打开\_通道\_响应**](https://msdn.microsoft.com/library/windows/hardware/ff536627)请求。 值的基础**响应**的成员[  **\_BRB\_SCO\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536870)结构与此请求一起传递，服务器配置文件驱动程序接受或拒绝连接请求。

4.  如果服务器配置文件驱动程序接受连接，然后可以调用蓝牙驱动程序堆栈[ *SCO 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536772)中指定的那样**回调**的成员[  **\_BRB\_SCO\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536870)结构以通知 SCO 连接的任何更改的服务器配置文件驱动程序。

配置文件驱动程序接受连接请求后，它可以使用其他 BRBs 发送和接收数据，通过新建立的 SCO 连接。

若要停止接收通知的远程设备 SCO 连接尝试，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_SCO\_注销\_服务器** ](https://msdn.microsoft.com/library/windows/hardware/ff536630)请求来取消注册服务器时配置文件驱动程序处理[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)插删除通知。

有关通知和回调函数的详细信息，请参阅[支持蓝牙事件通知](supporting-bluetooth-event-notifications.md)。

 

 





