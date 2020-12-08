---
title: NDISWAN 概述
description: NDISWAN 概述
keywords:
- NDISWAN WDK 网络
- NDIS 中间驱动程序 WDK，NDISWAN 驱动程序
- 中间驱动程序 WDK 网络，NDISWAN 驱动程序
- 体系结构 WDK WAN，NDISWAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19f0cd924b9cc75eb38f958a0ff12a5fdb69be79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808605"
---
# <a name="ndiswan-overview"></a>NDISWAN 概述





NDISWAN 是系统提供的 NDIS 中间驱动程序，它提供 WAN 微型端口驱动程序使用的功能，如数据压缩、加密、环回和简单的 PPP 帧。 因此，需要 WAN 微型端口驱动程序来仅实现特定于中型 (的那些功能，例如，ISDN) 需要 Q931 信号。

下图显示了 NDISWAN 如何与 RAS 体系结构中的其他组件进行交互。

![说明 ndiswan 如何与 ras 体系结构中的其他组件进行交互的关系图](images/ndiswan-1.png)

为过量协议驱动程序，NDISWAN 将显示 NDIS 和 CoNDIS 微型端口驱动程序接口。 对于基础 WAN 微型端口驱动程序，NDISWAN 提供了包含一些特定于 WAN 的元素的 NDIS 和 CoNDIS 协议接口。

在 CoNDIS 环境中，WAN 微型端口驱动程序可以是面向连接的微型端口驱动程序，也可以是集成的微型端口调用管理器 (MCM) 。

NDISWAN 提供以下功能：

-   **数据包转换**

    NDISWAN 将协议驱动程序从 LAN 传递给它的发送数据包转换为 PPP 格式。 NDISWAN 对通过 WAN 微型端口驱动程序传递给它的接收数据包执行反向转换。 NDISWAN 使用简单的 HDLC 组帧。 大多数特定于介质的帧必须由微型端口驱动程序完成。 有关 WAN 数据包帧的详细信息，请参阅 [Wan 数据包组帧](wan-packet-framing.md)。

-   **数据包处理**

    发送数据包包括标头压缩、数据压缩和加密的配置选项。 NDISWAN 在发送数据包时按顺序应用这些操作。 NDISWAN 按接收数据包的反向顺序应用这些选项。 如果 NDISWAN 确定配置选项（如压缩或加密）已启用，则 NDISWAN 将发送 OID 以通知底层 WAN 微型端口驱动程序。

-   **简化的驱动程序绑定**

    NDISWAN 简化了协议驱动程序和 WAN 微型端口驱动程序之间的绑定。 有关 WAN 驱动程序绑定的详细信息，请参阅 [Wan 驱动程序绑定和连接](wan-driver-bindings-and-connections.md)。

-   **数据转发**

    在 NDIS WAN 环境中，NDISWAN 检查发送数据包描述符的标头，并确定数据包将发送到的链接。 NDISWAN 将数据包复制到一个连续的缓冲区中，并将其转发到基础微型端口驱动程序。 在 CoNDIS WAN 环境中，NDISWAN 根据数据包的关联虚拟连接转发数据包 (VC) 。 有关 WAN 驱动程序链接和连接的详细信息，请参阅 [Wan 驱动程序绑定和连接](wan-driver-bindings-and-connections.md)。

 

 





