---
title: 在蓝牙配置文件驱动程序中接受 L2CAP 连接
description: 在蓝牙配置文件驱动程序中接受 L2CAP 连接
ms.assetid: 26a8238d-717a-438f-84d0-047ce9618928
keywords:
- L2CAP 配置文件驱动程序 WDK 蓝牙
- 逻辑链路控制器和适配协议 WDK 蓝牙
- 传入 L2CAP 连接请求 WDK 蓝牙
- 连接 WDK 蓝牙
- 远程连接通知 WDK 蓝牙
- 通知 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b13666b3dcefaa9d3bd8592bf895748120cb97e
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010353"
---
# <a name="accepting-l2cap-connections-in-a-bluetooth-profile-driver"></a>在蓝牙配置文件驱动程序中接受 L2CAP 连接


L2CAP 服务器配置文件驱动程序响应来自远程设备的传入逻辑链接控制和适配协议 (L2CAP) 连接请求。 例如，PDA 的 L2CAP 服务器配置文件驱动程序将响应 PDA 的传入连接请求。

**接收传入 L2CAP 连接请求**

1.  **若要接收来自特定 PSM 的*任何*远程设备的传入 L2CAP 连接请求**，配置文件驱动程序应首先[构建并发送](building-and-sending-a-brb.md) [**BRB \_ L2CA \_ REGISTER \_ Server**](/previous-versions/ff536618(v=vs.85))请求，并在**BtAddress**成员中指定**NULL** ，并在请求的**Psm** \_ BRB \_ L2CA \_ 注册 \_ 服务器结构的 PSM 成员中指定0。 发送**BRB \_ L2CA \_ register \_ 服务器**请求时，配置文件驱动程序还必须向蓝牙驱动程序堆栈注册[*L2CAP 回调函数*](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)。 这会使蓝牙驱动程序堆栈通知传入 L2CAP 连接请求的配置文件驱动程序。

    然后，配置文件驱动程序应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ REGISTER \_ PSM**](/previous-versions/ff536621(v=vs.85)) 请求，以便蓝牙驱动程序堆栈接受来自请求注册的 psm 的连接。 否则，蓝牙驱动程序堆栈会拒绝所有具有未知 (的连接请求) 的连接请求。 有关 PSMs 的详细信息，请参阅[** \_ BRB \_ PSM**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_psm)结构。

2.  **若要从*特定*的远程设备/PSM 对接收传入的 L2CAP 连接请求**，配置文件驱动程序应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ L2CA \_ REGISTER \_ server**](/previous-versions/ff536618(v=vs.85)) 请求，在 **BtAddress** 成员中指定远程设备的地址，并在 **psm** 成员中指定该请求的伴随 \_ BRB \_ L2CA \_ 注册 \_ 服务器结构的 psm。 发送**BRB \_ L2CA \_ register \_ 服务器**请求时，配置文件驱动程序还必须向蓝牙驱动程序堆栈注册[*L2CAP 回调函数*](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)。 这会使蓝牙驱动程序堆栈通知传入 L2CAP 连接请求的配置文件驱动程序。

3.  配置文件驱动程序应发出 [**IOCTL \_ BTH \_ SDP \_ 提交 \_ 记录**](/windows-hardware/drivers/ddi/bthioctl/ni-bthioctl-ioctl_bth_sdp_submit_record)。 然后，配置文件驱动程序可以注册一个 SDP 记录，用于描述配置文件驱动程序支持的服务，以便远程系统可以使用 SDP 发现新服务。

4.  当蓝牙驱动程序堆栈从远程设备收到传入 L2CAP 连接请求时，蓝牙驱动程序堆栈会调用先前由配置文件驱动程序注册的 [*L2CAP 回调函数*](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback) 。 蓝牙驱动程序堆栈将值 **IndicationRemoteConnect** 传递给回调函数的 *指示* 参数。

5.  为了响应传入连接请求，配置文件驱动程序应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ L2CA \_ OPEN \_ 通道 \_ 响应**](/previous-versions/ff536616(v=vs.85)) 请求。 服务器配置文件驱动程序使用从回调函数的 *Parameters* 参数中的蓝牙驱动程序堆栈传递的值来协商与远程设备的连接设置。 根据与此请求一起传递的[** \_ BRB \_ L2CA \_ 打开 \_ 通道**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)结构的**响应**成员的值，服务器配置文件驱动程序接受或拒绝连接请求。

6.  如果服务器配置文件驱动程序接受连接，则蓝牙驱动程序堆栈可以调用[*L2CAP 回调函数*](/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbthport_indication_callback)，如[** \_ BRB \_ L2CA \_ 开放 \_ 通道**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)结构的**回调**成员中所指定的那样。 蓝牙驱动程序堆栈使用此函数通知服务器配置文件驱动程序对 L2CAP 连接进行的任何更改。

**注意**  
-   单个配置文件驱动程序可以通过构建并发送多个 **BRB \_ L2CA \_ register \_ SERVER** 请求来接收来自多个不同远程设备/PSM 对的传入 L2CAP 连接请求，并在请求的 **BtAddress** 和 **psm** 成员中指定唯一远程设备地址和 psm 对。

-   单个配置文件驱动程序可以注册以接收来自特定 PSM 的 *任何* 远程设备的传入 L2CAP 连接请求，还可以从多个不同的远程设备/psm 对接收传入的 L2CAP 连接请求，方法是先注册以接收来自特定 PSM 的任何远程设备的传入 L2CAP 连接请求，然后注册以接收来自特定远程设备/PSM 对的传入 L2CAP 连接请求，只要第一步中注册的特定 PSM 并未再次注册。

-   多个配置文件驱动程序无法注册为同一 PSM 的任何远程设备接收传入 L2CAP 连接请求。 Bluetooth 驱动程序堆栈只允许一个配置文件驱动程序接收来自特定 PSM 的任何远程设备的传入 L2CAP 连接请求。

 

配置文件驱动程序接受连接请求后，它可以使用其他 BRBs 通过新建立的 L2CAP 连接来发送和接收数据。

若要停止接收远程设备 L2CAP 连接尝试的通知，配置文件驱动程序应在配置文件驱动程序处理[**IRP \_ MN \_ 删除 \_ 设备**](../kernel/irp-mn-remove-device.md)即插即用删除通知时，[生成并发送](building-and-sending-a-brb.md) [**BRB \_ L2CA \_ 取消 \_ **](/previous-versions/ff536619(v=vs.85))注册服务器的请求。

有关通知和回调函数的详细信息，请参阅 [支持蓝牙事件通知](supporting-bluetooth-event-notifications.md)。

 

