---
title: WAN 驱动程序绑定和连接
description: WAN 驱动程序绑定和连接
ms.assetid: e91bbdaf-9826-4031-a877-73f3e099a1e4
keywords:
- NDISWAN WDK 网络
- WAN 微型端口驱动程序 WDK 网络连接
- 绑定 WDK WAN
- WDK WAN 连接
- WDK WAN，绑定体系结构
- WDK WAN，连接的体系结构
- WAN 微型端口驱动程序 WDK 网络绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58637a4455936743b900d393d7e09deec6231397
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566936"
---
# <a name="wan-driver-bindings-and-connections"></a>WAN 驱动程序绑定和连接





本主题概述了绑定和 NDISWAN、 基础协议驱动程序和基础 WAN 微型端口驱动程序之间的连接。

### <a name="bindings"></a>绑定

NDISWAN 将绑定到一个或更多 WAN 微型端口驱动程序和一个或多个协议驱动程序绑定到 NDISWAN。

下图说明了 WAN 的客户端协议驱动程序、 NDISWAN 和 WAN 之间的绑定关系微型端口驱动程序。

![说明 wan 的客户端协议驱动程序、 ndiswan 和 wan 微型端口驱动程序之间的绑定关系的关系图](images/209-04.png)

协议驱动程序将绑定到 NDISWAN 的一次，并不将绑定到 WAN 的微型端口驱动程序。 此类型的绑定节省内存，并简化了 WAN 微型端口驱动程序。 由于通常有多个协议驱动程序中给定的系统，并且可能有多个 WAN 微型端口驱动程序，绑定数的减少节省内存。 也就是说，每个协议没有要绑定到每个 WAN 微型端口驱动程序。 此外，因为协议驱动程序可以依赖于仅具有单个 WAN 绑定，可以简化这些协议驱动程序。

### <a name="connections"></a>连接

NDIS WAN 和 WAN 的 CoNDIS 微型端口驱动程序实现用于连接的不同模型：

-   NDIS WAN 的微型端口驱动程序使用链接来发送和接收数据。 链接是逻辑，点到点的双向通信通道。 可以有许多链接，每个 nic。 链接动态建立并销毁。 链接速度和质量的链接而异的每个连接。 但是，填充和链接参数必须是相同的 NIC 支持的所有链接。 例如，如果 NDIS WAN 的微型端口驱动程序指定一个 20 字节的标头填充和 4 字节尾部填充，此填充必须保持不变的微型端口驱动程序的 NIC 支持的所有链接。

-   CoNDIS WAN 的微型端口驱动程序通过发送和接收数据 (VCs) 的虚拟连接。 可以有多个 VCs 每个 nic。 数据传输速度可能会变化 VC VC，而其他 VC 参数都是相同的 NIC 支持的所有 VCs。 CoNDIS WAN 的微型端口驱动程序可以指定任何网络数据包的微型端口驱动程序可以发送和接收的最大帧大小。 如果微型端口驱动程序指定最大帧大小，该最大帧大小必须保持不变的所有 VCs 上该 nic。

像其他微型端口驱动程序中，每个 WAN 微型端口驱动程序必须具有为其分配和维护特定于 NIC 的上下文区域的至少一个 NIC。 特定于 NIC 的上下文区域是一种简单方式来存储、 检索和使用的 NIC （如中断、 总线类型、 I/O 范围和内存） 的具体硬件情况有关的信息和维护连接的运行时状态。 微型端口驱动程序应指定一个特定于 NIC 的上下文区域的每个网络卡，它支持在系统中。

如果特定的 WAN 微型端口驱动程序指定它不需要 PPP 地址和控件字段压缩，则假定为微型端口驱动程序的 nic 的所有连接，则返回 true

WAN 微型端口驱动程序可以发送或广域网上接收数据包之前，必须创建连接：

-   在 NDIS 环境中，应用程序必须设置连接上发送的节点，或接受连接的建立或接受调用源自远程节点上。 安装程序、 监督和关闭的连接均通过 TAPI。 TAPI 请求和向 TAPI 所有状态指示经历 NDISTAPI。 有关 TAPI 和 NDISTAPI 的详细信息，请参阅[NDISTAPI 概述](ndistapi-overview.md)。

-   在的 CoNDIS 环境中，必须创建 VC。 NDPROXY 驱动程序创建应用程序产生的传出调用的 VC。 同样，呼叫管理器 （或 MCM） 启动对 NDISWAN 和 NDPROXY 呼叫管理器指示的传入呼叫的 VC 的创建。 呼叫管理器必须进行通信，并有时协商与远程方 VC 参数。 安装程序、 监督和关闭的连接均通过 TAPI。 TAPI 请求和向 TAPI 所有状态指示经历 NDPROXY。 有关 TAPI 和 NDPROXY 的详细信息，请参阅[NDPROXY 概述](ndproxy-overview.md)。

 

 





