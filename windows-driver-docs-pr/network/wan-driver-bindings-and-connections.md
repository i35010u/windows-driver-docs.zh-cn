---
title: WAN 驱动程序绑定和连接
description: WAN 驱动程序绑定和连接
keywords:
- NDISWAN WDK 网络
- WAN 微型端口驱动程序 WDK 网络，连接
- 绑定 WDK WAN
- 连接 WDK WAN
- 体系结构 WDK WAN，绑定
- 体系结构 WDK WAN，连接
- WAN 微型端口驱动程序 WDK 网络，绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392feaa45a95729288aafade9436dbde4f1e0abc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839989"
---
# <a name="wan-driver-bindings-and-connections"></a>WAN 驱动程序绑定和连接





本主题概述了 NDISWAN、过量协议驱动程序和基础 WAN 微型端口驱动程序之间的绑定和连接。

### <a name="bindings"></a>绑定

NDISWAN 绑定到一个或多个 WAN 微型端口驱动程序，并将一个或多个协议驱动程序绑定到 NDISWAN。

下图说明了 WAN 客户端协议驱动程序、NDISWAN 和 WAN 微型端口驱动程序之间的绑定关系。

![说明 wan 客户端协议驱动程序、ndiswan 和 wan 微型端口驱动程序之间的绑定关系的示意图](images/209-04.png)

协议驱动程序将一次绑定到 NDISWAN，并且不绑定到 WAN 微型端口驱动程序。 这种类型的绑定可节省内存并简化 WAN 微型端口驱动程序。 由于给定系统中通常存在多个协议驱动程序，并且可能有多个 WAN 微型端口驱动程序，因此减少了绑定数可以节省内存。 也就是说，每个协议不必绑定到每个 WAN 微型端口驱动程序。 此外，由于协议驱动程序只能依赖于单个 WAN 绑定，因此可以简化这些协议驱动程序。

### <a name="connections"></a>连接

NDIS WAN 和 CoNDIS WAN 微型端口驱动程序为连接实现不同的模型：

-   NDIS WAN 微型端口驱动程序使用链接来发送和接收数据。 链接是逻辑的点到点双向通信通道。 每个 NIC 可以有多个链接。 动态建立并断开链接。 每个连接的链接速度和质量可能会有所不同。 但是，对于 NIC 支持的所有链接，填充和链接参数必须相同。 例如，如果 NDIS WAN 微型端口驱动程序指定了20个字节的标头填充和4个字节的尾填充，则该填充必须保持为微型端口驱动程序的 NIC 支持的所有链接。

-   CoNDIS WAN 微型端口驱动程序通过虚拟连接 (VCs) 发送和接收数据。 每个 NIC 可以有多个 VCs。 尽管数据传输速度可能会不同于 VC，但其他 VC 参数对于 NIC 支持的所有 VCs 都是相同的。 CoNDIS WAN 微型端口驱动程序可以指定微型端口驱动程序可发送和接收的任何网络包的最大帧大小。 如果微型端口驱动程序指定了最大帧大小，则对于该 NIC 上的所有 VCs，最大帧大小必须保持不变。

与其他微型端口驱动程序一样，每个 WAN 微型端口驱动程序必须至少具有一个要为其分配和维护 NIC 特定上下文区域的 NIC。 NIC 特定的上下文区域只是一种方法，用于存储、检索和使用有关 NIC 的硬件细节的信息 (例如中断、总线类型、i/o 范围和内存) 并维护连接的运行时状态。 小型端口驱动程序应为其支持的系统中的每个网卡指定一个 NIC 特定的上下文区域。

如果特定的 WAN 微型端口驱动程序指定它不需要 PPP 地址和控制字段压缩，则会假设微型端口驱动程序 NIC 上的所有连接都采用 true。

必须先创建连接，然后 WAN 微型端口驱动程序才能在广域网上发送或接收数据包：

-   在 NDIS 环境中，应用程序必须设置一个连接，该连接是在发送节点上发出的，或者通过发出或接受调用来接受源自远程节点的连接。 通过 TAPI 完成设置、监督和断开连接。 Tapi 请求和 TAPI 的状态指示都通过 NDISTAPI。 有关 TAPI 和 NDISTAPI 的详细信息，请参阅 [NDISTAPI 概述](ndistapi-overview.md)。

-   在 CoNDIS 环境中，必须创建 VC。 NDPROXY 驱动程序为应用程序发出的传出调用创建一个 VC。 同样，呼叫管理器 (或 MCM) 为调用管理器指示 NDISWAN 和 NDPROXY 的传入呼叫启动创建 VC。 呼叫管理器必须进行通信，有时会与远程方协商 VC 的参数。 通过 TAPI 完成设置、监督和断开连接。 Tapi 请求和 TAPI 的状态指示都通过 NDPROXY。 有关 TAPI 和 NDPROXY 的详细信息，请参阅 [NDPROXY 概述](ndproxy-overview.md)。

 

 





