---
title: 创建到远程设备的 L2CAP 客户端连接
description: 创建到远程设备的 L2CAP 客户端连接
keywords:
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 异步 Connection-Less WDK 蓝牙
- ACL WDK 蓝牙
- L2CAP 配置文件驱动程序 WDK 蓝牙
- 逻辑链路控制器和适配协议 WDK 蓝牙
- 连接 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb94a2d6da727957ff06b3308945c71f719544a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798545"
---
# <a name="creating-a-l2cap-client-connection-to-a-remote-device"></a>创建到远程设备的 L2CAP 客户端连接


L2CAP 客户端配置文件驱动程序是一个配置文件驱动程序，该驱动程序 (ACL) 连接到远程设备，请求异步无连接链接。 如果设备接受连接，则会通知 L2CAP 客户端配置文件驱动程序对连接的任何更改。 例如，L2CAP 客户端配置文件驱动程序可以请求与远程打印机的连接，并且在打印机接受该请求后，当关闭或删除打印机后，蓝牙驱动程序堆栈可以通知配置文件驱动程序。

L2CAP 客户端配置文件驱动程序必须具有有关远程设备的信息，例如，设备使用的协议/服务多路复用器 (PSM) ，以便请求与设备的连接。 客户端配置文件驱动程序可以通过服务发现协议 (SDP) DDIs 或通过服务的固定 PSM 获取此信息。 有关如何获取此信息的详细信息，请参阅 [访问 SDP 服务信息](accessing-sdp-service-information.md)。

若要启动到远程设备的 L2CAP 连接，请在客户端配置文件驱动程序包含设备所需的信息后，它应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ L2CA \_ OPEN \_ 通道**](/previous-versions/ff536615(v=vs.85)) 请求。

当客户端配置文件驱动程序生成请求时，它将提供一个指针，该指针指向 **Argument1 参数** 关联的 [**\_ BRB \_ L2CA \_ 开放 \_ 通道**](/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)结构。 此结构包含远程设备的蓝牙地址、为设备注册的 PSM 以及其他配置参数。

如果远程设备接受开放通道请求，则 BRB L2CA 开放式通道结构的 **OutResults** 和 **InResults** 成员 \_ \_ \_ \_ 包含有关新创建的连接的信息。 **OutResults** 成员指定通道的出站半个参数， **InResults** 成员指定通道的入站半部分的参数。

在 BRB L2CA 开放通道结构中传递的几个配置值（ \_ \_ \_ \_ 如 **Mtu** 成员）用于协商与远程设备的连接。 客户端配置文件驱动程序应提供尽可能宽的范围，以提高通道协商成功的几率。 指定最小消息传输单位 (MTU) 大于基本蓝牙最小 MTU 大小的大小仅在绝对必要时才执行。 如果协商失败，连接将失败。

**IncomingQueueDepth** \_ BRB \_ L2CA \_ 开放式通道结构的 IncomingQueueDepth 成员 \_ 指定在蓝牙驱动程序堆栈开始丢弃它们之前，蓝牙驱动程序堆栈将在连接上接收和排队的最大 mtu 数。 将此值设置为非常小的数字会增加数据丢失的几率，而将其设置为非常大的数字会增加内存需求。 Microsoft 建议将此成员设置为10。

当配置文件驱动程序不再需要 L2CAP 连接到远程设备时，它应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ L2CA \_ CLOSE \_ 通道**](/previous-versions/ff536614(v=vs.85)) 请求。

 

