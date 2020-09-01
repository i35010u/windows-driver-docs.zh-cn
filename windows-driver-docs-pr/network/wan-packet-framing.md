---
title: WAN 数据包分帧概述
description: WAN 数据包分帧概述
ms.assetid: 11a6fbf5-c7a9-474b-811e-c77a36e834f3
keywords:
- WAN 微型端口驱动程序 WDK 网络，数据包
- CoNDIS WAN 驱动程序 WDK 网络，数据包
- 数据包帧 WDK WAN
- NDISWAN WDK 网络
- WAN 数据包帧 WDK 网络
- 数据包帧 WDK WAN，关于 WAN 数据包组帧
- Wan packet 组帧 WDK 网络，关于 WAN 数据包组帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1949975820e3b076f50ec26930bd4771e764c3b6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209623"
---
# <a name="wan-packet-framing-overview"></a>WAN 数据包分帧概述





本部分提供有关 WAN 数据包帧的信息。

NDISWAN 中间驱动程序检索有关 WAN 微型端口驱动程序执行的 WAN 数据包组帧的信息，从微型端口驱动程序的响应到 [OID \_ WAN \_ 中型 \_ 子类型](/previous-versions/windows/hardware/network/ff561216(v=vs.85)) 查询信息请求。

NDISWAN 将传出数据包从 LAN 转换为 PPP 格式。 NDISWAN 使用简单的 HDLC 组帧。 大多数特定于介质的帧必须由微型端口驱动程序完成。

在将数据包发送到 WAN 微型端口驱动程序的 send 函数之前，NDISWAN 执行简单的 PPP HDLC 组帧。 简单的 PPP HDLC 组帧是 PPP 的 HDLC 组帧，没有 FCS、位或字节堆砌以及任何开始或结束标志。

以下主题提供有关 WAN 数据包组帧的其他信息：

[异步分帧](asynchronous-framing.md)

[ISDN 和交换网-56K 帧](isdn-and-switched-56k-framing.md)

 

