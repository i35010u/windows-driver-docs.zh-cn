---
title: NDISWAN 概述
description: NDISWAN 概述
ms.assetid: bc092222-5418-4a57-9811-5d97c1c10a73
keywords:
- NDISWAN WDK 网络
- NDIS 中间驱动程序 WDK、 NDISWAN 驱动程序
- 中间驱动程序 WDK 网络 NDISWAN 驱动程序
- 体系结构 WDK WAN NDISWAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6a9982052d9d98523bff1a205612b96eac0a632
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392404"
---
# <a name="ndiswan-overview"></a>NDISWAN 概述





NDISWAN 是一个系统提供 NDIS 中间驱动程序提供功能，例如数据压缩、 加密、 环回、 和 WAN 微型端口驱动程序使用的简单 PPP 帧。 因此需要 WAN 微型端口驱动程序来实现特定于该介质功能 （例如，Q931 信号则需要为 ISDN）。

下图显示了 NDISWAN 与 RAS 体系结构中的其他组件的接口。

![说明如何 ndiswan 接口与 ras 体系结构中其他组件的关系图](images/ndiswan-1.png)

过量协议驱动程序，到 NDISWAN 呈现 NDIS 和 CoNDIS 微型端口驱动程序接口。 基础 WAN 微型端口驱动程序，到 NDISWAN 显示 NDIS 和 CoNDIS 协议界面，包括某些特定于 WAN 的元素。

在的 CoNDIS 环境中，WAN 微型端口驱动程序可以是面向连接的微型端口驱动程序或集成的微型端口呼叫管理器 (MCM)。

NDISWAN 提供了以下功能：

-   **数据包转换**

    NDISWAN 将发送给它的协议驱动程序将从传递 LAN 到 PPP 格式的数据包。 NDISWAN 执行反向转换，则为接收数据包传递给它的 WAN 微型端口驱动程序。 NDISWAN 使用简单 HDLC 组帧。 必须由微型端口驱动程序完成大部分特定于媒体的帧。 有关 WAN 数据包分帧的详细信息，请参阅[WAN 数据包分帧](wan-packet-framing.md)。

-   **数据包处理**

    发送的数据包包括标头压缩、 数据压缩和加密的配置选项。 NDISWAN 上发送数据包应用这些操作的顺序。 NDISWAN 应用这些选项的相反顺序在接收数据包。 如果 NDISWAN 确定启用了压缩或加密等的配置选项，NDISWAN 发送 OID 来通知基础 WAN 微型端口驱动程序。

-   **驱动程序的简化的绑定**

    NDISWAN 简化了协议驱动程序和 WAN 微型端口驱动程序之间的绑定。 有关 WAN 驱动程序绑定的详细信息，请参阅[WAN 驱动程序绑定和连接](wan-driver-bindings-and-connections.md)。

-   **数据转发**

    在 NDIS WAN 环境中，NDISWAN 检查发送数据包的描述符标头，并确定将对其发送链接该数据包。 NDISWAN 将数据包复制到连续缓冲区，并将其转发到基础微型端口驱动程序。 在的 CoNDIS WAN 环境中，根据数据包的关联的虚拟连接 (VC) 数据包将转发 NDISWAN。 有关驱动程序 WAN 链接和连接的详细信息，请参阅[WAN 驱动程序绑定和连接](wan-driver-bindings-and-connections.md)。

 

 





