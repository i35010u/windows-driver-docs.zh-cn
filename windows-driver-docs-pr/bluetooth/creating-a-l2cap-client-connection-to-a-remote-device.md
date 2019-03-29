---
title: 创建到远程设备的 L2CAP 客户端连接
description: 创建到远程设备的 L2CAP 客户端连接
ms.assetid: b279db4b-3a4e-407e-ae9b-7330af1905b4
keywords:
- SDP WDK 蓝牙
- 服务发现协议 WDK 蓝牙
- 异步无连接的 WDK 蓝牙
- ACL WDK 蓝牙
- L2CAP 配置文件驱动程序 WDK 蓝牙
- 逻辑链接控制器和适应协议 WDK 蓝牙
- 连接 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65b3495e988217221753546a2a76c26b683f99a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567981"
---
# <a name="creating-a-l2cap-client-connection-to-a-remote-device"></a>创建到远程设备的 L2CAP 客户端连接


L2CAP 客户端配置文件驱动程序是请求异步无连接链接 (ACL) 连接到远程设备的配置文件驱动程序。 如果设备接受连接，连接到任何更改通知 L2CAP 客户端配置文件驱动程序。 例如，L2CAP 客户端配置文件驱动程序可以请求连接到远程打印机和打印机接受请求后，可以在打印机处于关闭状态时通知配置文件驱动程序的蓝牙驱动程序堆栈，或删除。

L2CAP 客户端配置文件驱动程序必须具有远程设备，如协议/服务多路复用器 (PSM) 设备时使用，若要请求到设备的连接信息。 客户端配置文件驱动程序可以获取此信息通过服务发现协议 (SDP) DDIs，或通过服务的固定 PSM。 有关如何获取此信息的详细信息，请参阅[访问 SDP 服务信息](accessing-sdp-service-information.md)。

若要启动的 L2CAP 连接到远程设备时，客户端配置文件驱动程序具有关于设备的所需的信息后，它应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_L2CA\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536615)请求。

当客户端配置文件驱动程序生成请求时，它提供一个指向[  **\_BRB\_L2CA\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536860)中结构**Parameters.Others.Argument1**与请求关联的 IRP 的成员。 此结构包含远程设备的蓝牙地址，PSM 注册的设备，以及其他配置参数。

如果远程设备接受打开通道请求**OutResults**并**InResults**的成员\_BRB\_L2CA\_打开\_通道结构包含新创建的连接有关的信息。 **OutResults**成员指定通道的出站另一半的参数和**InResults**成员指定通道的入站另一半的参数。

多个传递中的配置值\_BRB\_L2CA\_打开\_通道的结构，如**Mtu**成员，用于协商与远程连接设备。 客户端配置文件驱动程序应提供作为宽的范围，可以增加成功通道协商的可能性。 指定最小消息传输单位 (MTU) 大小超过基本蓝牙最小 MTU 大小仅应在绝对必要时。 如果协商失败，则连接将失败。

**IncomingQueueDepth**的成员\_BRB\_L2CA\_打开\_通道结构指定 Mtu 的蓝牙驱动程序堆栈将接收并在队列的最大数目之前驱动程序堆栈开始弃用这些蓝牙连接。 此值设置为非常小的数值增加的数据丢失，而将其设置为非常大的数会增加内存需求。 Microsoft 建议将此成员设置为 10。

当配置文件驱动程序不再需要 L2CAP 连接到远程设备时，它应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_L2CA\_关闭\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536614)请求。

 

 





