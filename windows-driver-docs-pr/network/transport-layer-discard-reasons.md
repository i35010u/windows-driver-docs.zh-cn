---
title: 传输层丢弃原因
description: 本部分描述了 Windows 筛选平台标注驱动程序的传输层放弃原因。
ms.assetid: e2a9dcd1-87c6-4052-ae96-3a7994328dd0
keywords:
- 传输层放弃原因网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5008e6eb284ba76b671909b1e1a01aeed12fe001
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358381"
---
# <a name="transport-layer-discard-reasons"></a>传输层丢弃原因

标识符的数据将被放弃由一个传输层的可能原因如下所示。 这些标识符是 Fwpsk.h 中定义的 INET_DISCARD_REASON 枚举中的常量值。

| 放弃原因标识符 | 放弃原因说明 |
| --- | --- |
| InetDiscardSourceUnspecified | 传出数据包的源地址未指定。 |
| InetDiscardDestinationMulticast | 传出数据包的目标地址是未指定的地址，并传输不支持多播的地址。 |
| InetDiscardHeaderInvalid | 数据包的传输协议标头无效。 |
| InetDiscardChecksumInvalid | 数据包的传输协议标头中的校验和无效。 |
| InetDiscardEndpointNotFound | 找不到数据包的标头中指定的终结点。 |
| InetDiscardConnectedPath | 数据包的远程地址不匹配的远程地址的连接的终结点。 |
| InetDiscardSessionState | 无法基于网络层信息传递该数据包。 |
| InetDiscardReceiveInspection | 连接已关闭由于接收检查失败。 |
| InetDiscardAckInvalid | 数据包是无效的 ACK 段。 |
| InetDiscardExpectedSyn | 应有 SYN 段。 |
| InetDiscardRst | 数据包是无效的 RST 段。 |
| InetDiscardSynRcvdSyn | SYN_RCVD 状态中的 TCP 连接接收到另一个 SYN 段。 |
| InetDiscardSimultaneousConnect | TCP 连接遇到 simultaneous-connect 条件。 |
| InetDiscardPawsFailed | TCP PAW 检查失败。 |
| InetDiscardLandAttack | 数据包被检测为 Land 攻击的一部分。 |
| InetDiscardMissedReset | 在接收时段外的 SYN 段 SYN_RCVD 连接上收到。 RST 可能已丢失。 |
| InetDiscardOutsideWindow | TCP 段已接收窗口外。 |
| InetDiscardDuplicateSegment | 收到重复的 TCP 段。 |
| InetDiscardClosedWindow | TCP 接收窗口已关闭。 |
| InetDiscardTcbRemoved | TCP 连接已关闭。 |
| InetDiscardFinWait2 | 正在关闭 TCP 连接。 |
| InetDiscardReassemblyConflict | 遇到 FIN 段的接收 TCP 数据重组冲突。 |
| InetDiscardFinReceived | FIN 已接收的 TCP 连接;可接收没有更多数据。 |
| InetDiscardListenerInvalidFlags | 侦听的 TCP 套接字接收一个段具有无效的标志。 |
| InetDiscardUrgentDeliveryAllocationFailure | 没有足够的内存 URG 传递 TCP 连接上。 |
| InetDiscardTcbNotInTcbTable | 由于紧急交付，TCP 连接已关闭。 |
| InetDiscardTimeWaitTcbReceivedRstOutsideWindow | TIME_WAIT 状态 TCP 连接接收在时段外的 RSP 段。 |
| InetDiscardTimeWaitTcbSynAndOtherFlags | TIME_WAIT 状态 TCP 连接收到与 SYN 段和一个或多个不兼容的标志。 |
| InetDiscardTimeWaitTcb | TIME_WAIT 状态 TCP 连接接收到无效的段。 |

