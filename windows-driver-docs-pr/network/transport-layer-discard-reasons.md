---
title: 传输层丢弃原因
description: 本部分介绍 Windows 筛选平台标注驱动程序的传输层丢弃原因。
keywords:
- 传输层丢弃原因网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb8755bb786506cb9fb2b2b8698fa1bab33566ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837655"
---
# <a name="transport-layer-discard-reasons"></a>传输层丢弃原因

其中一个传输层丢弃数据的可能原因的标识符如下所示。 这些标识符是 Fwpsk 中定义的 INET_DISCARD_REASON 枚举中的常量值。

| 丢弃原因标识符 | 丢弃原因说明 |
| --- | --- |
| InetDiscardSourceUnspecified | 未指定传出数据包的源地址。 |
| InetDiscardDestinationMulticast | 传出数据包的目标地址是未指定的地址，并且传输不支持多播地址。 |
| InetDiscardHeaderInvalid | 数据包的传输协议标头无效。 |
| InetDiscardChecksumInvalid | 数据包的传输协议标头中的校验和无效。 |
| InetDiscardEndpointNotFound | 找不到数据包标头中指定的终结点。 |
| InetDiscardConnectedPath | 数据包远程地址与连接的终结点的远程地址不匹配。 |
| InetDiscardSessionState | 无法根据网络层信息传递数据包。 |
| InetDiscardReceiveInspection | 由于接收检查失败，连接被关闭。 |
| InetDiscardAckInvalid | 数据包是无效的确认段。 |
| InetDiscardExpectedSyn | 应为 SYN 段。 |
| InetDiscardRst | 数据包是无效的 RST 段。 |
| InetDiscardSynRcvdSyn | 处于 SYN_RCVD 状态的 TCP 连接收到另一个 SYN 段。 |
| InetDiscardSimultaneousConnect | TCP 连接遇到同时连接的情况。 |
| InetDiscardPawsFailed | TCP PAW 检查失败。 |
| InetDiscardLandAttack | 检测到数据包作为土地攻击的一部分。 |
| InetDiscardMissedReset | 在 SYN_RCVD 连接上接收到接收窗口外部的 SYN 段。 可能已丢失 RST。 |
| InetDiscardOutsideWindow | TCP 段在接收窗口之外。 |
| InetDiscardDuplicateSegment | 收到重复的 TCP 段。 |
| InetDiscardClosedWindow | TCP 接收窗口已关闭。 |
| InetDiscardTcbRemoved | TCP 连接已关闭。 |
| InetDiscardFinWait2 | TCP 连接正在关闭。 |
| InetDiscardReassemblyConflict | 接收 FIN 段时遇到 TCP 数据重汇编冲突。 |
| InetDiscardFinReceived | 已在 TCP 连接上收到 FIN;无法接收更多数据。 |
| InetDiscardListenerInvalidFlags | 侦听 TCP 套接字收到具有无效标志的段。 |
| InetDiscardUrgentDeliveryAllocationFailure | TCP 连接上的 URG 传递内存不足。 |
| InetDiscardTcbNotInTcbTable | 由于紧急传递，TCP 连接已关闭。 |
| InetDiscardTimeWaitTcbReceivedRstOutsideWindow | TIME_WAIT 状态 TCP 连接收到窗口外的 RSP 段。 |
| InetDiscardTimeWaitTcbSynAndOtherFlags | TIME_WAIT 状态 TCP 连接收到了包含 SYN 的段和一个或多个不兼容的标志。 |
| InetDiscardTimeWaitTcb | TIME_WAIT 状态 TCP 连接收到无效段。 |

