---
title: 网络层的放弃原因
description: 本部分描述了 Windows 筛选平台标注驱动程序的网络层放弃原因。 |
ms.assetid: 30066077-53ac-43bb-8c8b-67af210f747e
keywords:
- 网络层的放弃原因网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc51c3ca5788497cd7d005e740aae8e31fa61c2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526171"
---
# <a name="network-layer-discard-reasons"></a>网络层的放弃原因

标识符的数据将被放弃由一个网络层的可能原因如下所示。 这些标识符是 Fwpsk.h 中定义的 IP_DISCARD_REASON 枚举中的常量值。

| 放弃原因标识符 | 放弃原因说明 |
| --- | --- |
| IpDiscardBadSourceAddress | 传出数据包的源地址是多播的地址、 广播的地址，或包含嵌入的 IPv4 环回 IPv6 地址或未指定的地址。 |
| IpDiscardNotLocallyDestined | 已接收的数据包的目标地址不存在的系统上，并存在不适当转发接口。 |
| IpDiscardProtocolUnreachable | 任一没有传输协议处理程序接收的数据包或传输协议处理程序已拒绝处理数据包。 |
| IpDiscardPortUnreachable | 没有为接收数据包所接收的数据包的目标端口上的应用程序。 |
| IpDiscardBadLength | 所接收的数据包中指定的长度字段不一致，数据包的长度。 |
| IpDiscardMalformedHeader | 所接收的数据包包含可识别的扩展标头或其内容是无效的选项。 |
| IpDiscardNoRoute | 所接收的数据包无法转发到其目标地址，因为系统的路由表不包含指向该目标的路由。 |
| IpDiscardBeyondScope | 不能转发接收的数据包，因为数据包的传入和传出的网络接口具有不同的区域索引为数据包的区域级别。 |
| IpDiscardInspectionDrop | 由网络堆栈，保留供内部使用。 |
| IpDiscardTooManyDecapsulations | 所接收的数据包无法转发到其目标地址，因为有太多 decapsulations。 |
| IpDiscardAdministrativelyProhibited | 由网络堆栈，保留供内部使用。 |
| IpDiscardHopLimitExceeded | 已超过所接收的数据包的跃点限制或生存时间限制。 |
| IpDiscardAddressUnreachable | 将传出数据包无法发送到数据包的目标地址或者因为目标不存在或不允许的数据包发送到该目标。 |
| IpDiscardRscPacket | 无法发送传出的数据包，因为它是接收方合并 (RSC) 数据包。 |
| IpDiscardArbitrationUnhandled | 由网络堆栈，保留供内部使用。 |
| IpDiscardInspectionAbsorb | 无法发送传出的数据包，因为 WFP 花费了数据包的所有权。 |
| IpDiscardDontFragmentMtuExceeded | 由网络堆栈，保留供内部使用。 |
| IpDiscardBufferLengthExceeded | 由网络堆栈，保留供内部使用。 |
| IpDiscardAddressResolutionTimeout | 由网络堆栈，保留供内部使用。 |
| IpDiscardAddressResolutionFailure | 由网络堆栈，保留供内部使用。 |
| IpDiscardIpsecFailure | 由网络堆栈，保留供内部使用。 |
| IpDiscardExtensionHeadersFailure | 由网络堆栈，保留供内部使用。 |
| IpDiscardAllocationFailure | 由网络堆栈，保留供内部使用。 |

