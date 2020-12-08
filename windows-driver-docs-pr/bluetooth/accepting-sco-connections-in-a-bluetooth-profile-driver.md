---
title: 在蓝牙配置文件驱动程序中接受 SCO 连接
description: 在蓝牙配置文件驱动程序中接受 SCO 连接
keywords:
- 同步 Connection-Oriented WDK 蓝牙
- SCO profile 驱动程序 WDK 蓝牙
- 传入 SCO 连接请求 WDK 蓝牙
- 远程连接通知 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e4104ac8327cfe723f648b07833780856b88a1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784261"
---
# <a name="accepting-sco-connections-in-a-bluetooth-profile-driver"></a>在蓝牙配置文件驱动程序中接受 SCO 连接


SCO 配置文件驱动程序可以注册自身，以响应远程设备的传入同步 Connection-Oriented (SCO) 连接请求。 例如，适用于无绳电话服务配置文件的 SCO 配置文件驱动程序 (CTP) 设备从 CTP 设备响应传入 SCO 连接请求，接受或拒绝该请求。 如果服务器配置文件驱动程序接受该请求，则服务器配置文件驱动程序会响应设备输入，并将输入传递到蓝牙驱动程序堆栈。

服务器配置文件驱动程序必须执行以下步骤才能接受来自远程蓝牙设备的传入 SCO 连接请求。

**从远程设备接收传入的 SCO 连接请求**

1.  配置文件驱动程序应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ sco \_ register \_ SERVER**](/previous-versions/ff536628(v=vs.85)) 请求，以便向蓝牙驱动程序堆栈注册 [*SCO 回调函数*](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback) ，以便堆栈可以通知传入 SCO 连接请求的配置文件驱动程序。

2.  当蓝牙驱动程序堆栈从远程设备收到传入 SCO 连接请求时，它会调用先前由配置文件驱动程序注册的 [*Sco 回调函数*](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback) 。 蓝牙驱动程序堆栈将值 **ScoIndicationRemoteConnect** 传递给回调函数的 *指示* 参数。

3.  为了响应传入连接请求，配置文件驱动程序应生成并发送 [**BRB \_ SCO \_ 开放式 \_ 通道 \_ 响应**](/previous-versions/ff536627(v=vs.85)) 请求。 根据此请求传递的 [**\_ BRB \_ SCO \_ 开放式 \_ 通道**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)结构的 **响应** 成员的值，服务器配置文件驱动程序接受或拒绝连接请求。

4.  如果服务器配置文件驱动程序接受连接，则蓝牙驱动程序堆栈可以调用在 [**\_ BRB \_ SCO \_ 开放式 \_ 通道**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_sco_open_channel)结构的 **回调** 成员中指定的 [*SCO 回调函数*](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnsco_indication_callback)，以通知服务器配置文件驱动程序对 SCO 连接所做的任何更改。

配置文件驱动程序接受连接请求后，可以使用其他 BRBs 通过新建立的 SCO 连接来发送和接收数据。

若要停止接收远程设备 SCO 连接尝试的通知，配置文件驱动程序应在配置文件驱动程序处理 [**IRP \_ MN \_ 删除 \_ 设备**](../kernel/irp-mn-remove-device.md)即插即用删除通知时，[生成并发送](building-and-sending-a-brb.md) [**BRB \_ SCO \_ 取消 \_**](/previous-versions/ff536630(v=vs.85))注册服务器的请求。

有关通知和回调函数的详细信息，请参阅 [支持蓝牙事件通知](supporting-bluetooth-event-notifications.md)。

 

