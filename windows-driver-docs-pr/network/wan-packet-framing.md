---
title: WAN 数据包帧概述
description: WAN 数据包帧概述
ms.assetid: 11a6fbf5-c7a9-474b-811e-c77a36e834f3
keywords:
- WAN 微型端口驱动程序 WDK 网络, 数据包
- CoNDIS WAN 驱动程序 WDK 网络, 数据包
- 数据包帧 WDK WAN
- NDISWAN WDK 网络
- WAN 数据包帧 WDK 网络
- 数据包帧 WDK WAN, 关于 WAN 数据包组帧
- Wan packet 组帧 WDK 网络, 关于 WAN 数据包组帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33b1490e986bd03a1a8a33eb2e5581458a332aad
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565626"
---
# <a name="wan-packet-framing-overview"></a>WAN 数据包帧概述





本部分提供有关 WAN 数据包帧的信息。

NDISWAN 中间驱动程序检索有关 wan 微型端口驱动程序执行的 wan 数据包组帧的信息, 从微型端口驱动程序的响应到[\_OID\_WAN\_中型子类型](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff561216(v=vs.85))查询信息需要.

NDISWAN 将传出数据包从 LAN 转换为 PPP 格式。 NDISWAN 使用简单的 HDLC 组帧。 大多数特定于介质的帧必须由微型端口驱动程序完成。

在将数据包发送到 WAN 微型端口驱动程序的 send 函数之前, NDISWAN 执行简单的 PPP HDLC 组帧。 简单的 PPP HDLC 组帧是 PPP 的 HDLC 组帧, 没有 FCS、位或字节堆砌以及任何开始或结束标志。

以下主题提供有关 WAN 数据包组帧的其他信息:

[异步组帧](asynchronous-framing.md)

[ISDN 和交换网-56K 帧](isdn-and-switched-56k-framing.md)

 

 





