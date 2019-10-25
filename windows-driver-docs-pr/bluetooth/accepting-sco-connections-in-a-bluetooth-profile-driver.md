---
title: 在蓝牙配置文件驱动程序中接受 SCO 连接
description: 在蓝牙配置文件驱动程序中接受 SCO 连接
ms.assetid: 9736f113-26fb-4e2f-9a58-9874a11f8347
keywords:
- 面向同步连接的 WDK 蓝牙
- SCO profile 驱动程序 WDK 蓝牙
- 传入 SCO 连接请求 WDK 蓝牙
- 远程连接通知 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8433b71dee982cab1d93a8f56ea9e0469776e7b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833900"
---
# <a name="accepting-sco-connections-in-a-bluetooth-profile-driver"></a>在蓝牙配置文件驱动程序中接受 SCO 连接


SCO 配置文件驱动程序可以注册自身，以响应远程设备的传入同步连接定向（SCO）连接请求。 例如，无线电话服务配置文件（CTP）设备的 SCO 配置文件驱动程序响应来自 CTP 设备的传入 SCO 连接请求，接受或拒绝该请求。 如果服务器配置文件驱动程序接受该请求，则服务器配置文件驱动程序会响应设备输入，并将输入传递到蓝牙驱动程序堆栈。

服务器配置文件驱动程序必须执行以下步骤才能接受来自远程蓝牙设备的传入 SCO 连接请求。

**从远程设备接收传入的 SCO 连接请求**

1.  配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [**BRB\_SCO\_注册\_服务器**](https://docs.microsoft.com/previous-versions/ff536628(v=vs.85))请求以便向蓝牙驱动程序堆栈注册[*SCO 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)，以便堆栈可以通知传入 SCO 的配置文件驱动程序连接请求。

2.  当蓝牙驱动程序堆栈从远程设备收到传入 SCO 连接请求时，它会调用先前由配置文件驱动程序注册的[*Sco 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)。 蓝牙驱动程序堆栈将值**ScoIndicationRemoteConnect**传递给回调函数的*指示*参数。

3.  为了响应传入连接请求，配置文件驱动程序应生成并发送[**BRB\_SCO\_打开\_通道\_响应**](https://docs.microsoft.com/previous-versions/ff536627(v=vs.85))请求。 根据\_BRB 的**响应**成员的值[ **\_SCO\_打开**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)通过此请求传递\_通道结构，服务器配置文件驱动程序接受或拒绝连接请求。

4.  如果服务器配置文件驱动程序接受连接，则蓝牙驱动程序堆栈可以调用[ **\_BRB\_SCO\_开放\_通道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)结构的**回调**成员中指定的[*SCO 回调函数*](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)通知服务器配置文件驱动程序对 SCO 连接所做的任何更改。

配置文件驱动程序接受连接请求后，可以使用其他 BRBs 通过新建立的 SCO 连接来发送和接收数据。

若要停止接收远程设备 SCO 连接尝试的通知，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [**BRB\_SCO\_** ](https://docs.microsoft.com/previous-versions/ff536630(v=vs.85))在配置文件驱动程序处理[**时注销\_服务器请求以便注销服务器IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)即插即用删除通知。

有关通知和回调函数的详细信息，请参阅[支持蓝牙事件通知](supporting-bluetooth-event-notifications.md)。

 

 





