---
title: 创建到远程设备的 L2CAP 客户端连接
description: 创建到远程设备的 L2CAP 客户端连接
ms.assetid: b279db4b-3a4e-407e-ae9b-7330af1905b4
keywords:
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 异步连接-不减少 WDK 蓝牙
- ACL WDK 蓝牙
- L2CAP 配置文件驱动程序 WDK 蓝牙
- 逻辑链路控制器和适配协议 WDK 蓝牙
- 连接 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6982c879c0f31d002c913c6c9dffaef5f361ecfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833860"
---
# <a name="creating-a-l2cap-client-connection-to-a-remote-device"></a>创建到远程设备的 L2CAP 客户端连接


L2CAP 客户端配置文件驱动程序是一个配置文件驱动程序，用于请求与远程设备的异步无连接链接（ACL）连接。 如果设备接受连接，则会通知 L2CAP 客户端配置文件驱动程序对连接的任何更改。 例如，L2CAP 客户端配置文件驱动程序可以请求与远程打印机的连接，并且在打印机接受该请求后，当关闭或删除打印机后，蓝牙驱动程序堆栈可以通知配置文件驱动程序。

L2CAP 客户端配置文件驱动程序必须具有有关设备使用的远程设备（如协议/服务多路复用器（PSM））的信息，以便请求与设备的连接。 客户端配置文件驱动程序可以通过服务发现协议（SDP） DDIs 或通过服务的固定 PSM 获取此信息。 有关如何获取此信息的详细信息，请参阅[访问 SDP 服务信息](accessing-sdp-service-information.md)。

若要启动到远程设备的 L2CAP 连接，请在客户端配置文件驱动程序包含设备所需的信息后， [ **\_打开\_通道**](https://docs.microsoft.com/previous-versions/ff536615(v=vs.85))请求来[生成并发送](building-and-sending-a-brb.md)BRB\_L2CA。

当客户端配置文件驱动程序生成请求时，它将提供一个指向[ **\_BRB\_\_\_L2CA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_brb_l2ca_open_channel)的指针，该指针指向**Argument1 参数**关联的 IRP 的成员。 此结构包含远程设备的蓝牙地址、为设备注册的 PSM 以及其他配置参数。

如果远程设备接受开放通道请求，则 \_BRB\_L2CA\_\_的**OutResults**和**InResults**成员将包含有关新创建的连接的信息。 **OutResults**成员指定通道的出站半个参数， **InResults**成员指定通道的入站半部分的参数。

使用 \_BRB\_L2CA\_打开的几个配置值打开\_通道结构，如**Mtu**成员，用于协商与远程设备的连接。 客户端配置文件驱动程序应提供尽可能宽的范围，以提高通道协商成功的几率。 指定的最小消息传输单位（MTU）大小不能超过基本的蓝牙最小 MTU 大小，只应在绝对必要时才执行。 如果协商失败，连接将失败。

\_BRB\_\_\_L2CA 的**IncomingQueueDepth**成员在蓝牙驱动程序堆栈之前指定蓝牙驱动程序堆栈将接收并在连接上排队的最大 mtu 数开始丢弃它们。 将此值设置为非常小的数字会增加数据丢失的几率，而将其设置为非常大的数字会增加内存需求。 Microsoft 建议将此成员设置为10。

当配置文件驱动程序不再需要 L2CAP 连接到远程设备时，它应[生成并发送](building-and-sending-a-brb.md) [**BRB\_L2CA\_关闭\_通道**](https://docs.microsoft.com/previous-versions/ff536614(v=vs.85))请求。

 

 





