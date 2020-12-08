---
title: 网络层丢弃原因
description: 本部分介绍 Windows 筛选平台标注驱动程序的网络层丢弃原因。 |
keywords:
- 网络层丢弃原因网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d3bc9104ce1ab6bf22175dab669d15a284729ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792669"
---
# <a name="network-layer-discard-reasons"></a>网络层丢弃原因

其中一个网络层丢弃数据的可能原因的标识符如下所示。 这些标识符是 Fwpsk 中定义的 IP_DISCARD_REASON 枚举中的常量值。

| 丢弃原因标识符 | 丢弃原因说明 |
| --- | --- |
| IpDiscardBadSourceAddress | 传出数据包的源地址为多播地址、广播地址或包含嵌入的 IPv4 环回或未指定地址的 IPv6 地址。 |
| IpDiscardNotLocallyDestined | 接收的数据包的目标地址在系统中不存在，并且不存在适当的转发接口。 |
| IpDiscardProtocolUnreachable | 没有用于接收的数据包的传输协议处理程序，或者传输协议处理程序拒绝处理该数据包。 |
| IpDiscardPortUnreachable | 没有在接收的数据包的目标端口接收数据包的应用程序。 |
| IpDiscardBadLength | 在接收的数据包中指定的长度字段与数据包的长度不一致。 |
| IpDiscardMalformedHeader | 接收的数据包包含可识别的扩展标头或其内容无效的选项。 |
| IpDiscardNoRoute | 无法将收到的数据包转发到其目标地址，因为系统的路由表不包含到该目标的路由。 |
| IpDiscardBeyondScope | 无法转发收到的数据包，因为数据包的传入和传出网络接口具有不同的数据包区域级别的区域索引。 |
| IpDiscardInspectionDrop | 保留供网络堆栈内部使用。 |
| IpDiscardTooManyDecapsulations | 由于 decapsulations 太多，无法将收到的数据包转发到其目标地址。 |
| IpDiscardAdministrativelyProhibited | 保留供网络堆栈内部使用。 |
| IpDiscardHopLimitExceeded | 已超过接收的数据包的跃点限制或生存时间限制。 |
| IpDiscardAddressUnreachable | 无法将传出数据包发送到数据包的目标地址，原因可能是目标不存在，或者不允许将数据包发送到该目标。 |
| IpDiscardRscPacket | 无法发送传出数据包，因为它是接收方合并 (RSC) 数据包。 |
| IpDiscardArbitrationUnhandled | 保留供网络堆栈内部使用。 |
| IpDiscardInspectionAbsorb | 无法发送传出数据包，因为 WFP 取得了数据包的所有权。 |
| IpDiscardDontFragmentMtuExceeded | 保留供网络堆栈内部使用。 |
| IpDiscardBufferLengthExceeded | 保留供网络堆栈内部使用。 |
| IpDiscardAddressResolutionTimeout | 保留供网络堆栈内部使用。 |
| IpDiscardAddressResolutionFailure | 保留供网络堆栈内部使用。 |
| IpDiscardIpsecFailure | 保留供网络堆栈内部使用。 |
| IpDiscardExtensionHeadersFailure | 保留供网络堆栈内部使用。 |
| IpDiscardAllocationFailure | 保留供网络堆栈内部使用。 |

