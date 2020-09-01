---
title: 从 CoNDIS WAN 微型端口驱动程序发送数据包
description: 从 CoNDIS WAN 微型端口驱动程序发送数据包
ms.assetid: 66c42e90-e0d9-47d1-9e6d-cadb511bcb7a
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，数据包发送
- 环回 WDK 网络
- 软件环回 WDK 网络
- 混合模式环回 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7ad1d69b58d3f69c6331aa7bde664e95f44e9b1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214456"
---
# <a name="sending-packets-from-a-condis-wan-miniport-driver"></a>从 CoNDIS WAN 微型端口驱动程序发送数据包





上层驱动程序调用 [**NdisCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists) ，将网络数据包发送到网络 [** \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构列表中的基础 CoNDIS WAN 微型端口驱动程序。 NDISWAN 中间驱动程序 \_ \_ 从上层驱动程序转发这些网络缓冲区列表结构。 NDISWAN 在发送之前重新打包结构。 NDISWAN 将数据包转发到新的网络 \_ 缓冲区 \_ 列表结构。

NDISWAN 中间驱动程序调用 NDIS 来转发新的网络 \_ 缓冲区 \_ 列表结构，NDIS 调用 WAN 微型端口驱动程序的 [**MiniportCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists) 函数。

CoNDIS WAN 微型端口驱动程序拥有网络 \_ 缓冲区 \_ 列表结构和关联数据，直到发送完成。 小型端口驱动程序稍后必须调用 [**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) 来完成发送请求。

完成调用不一定表示网络 datahas 已传输;但除智能 Nic 外，网络数据通常已传输。 不过，完成调用会指示微型端口驱动程序已准备好释放网络 \_ 缓冲区列表结构的所有权 \_ 。

CoNDIS WAN 微型端口驱动程序收到 \_ \_ 包含网络数据包的网络缓冲区列表结构后，应将数据包发送到活动虚拟连接 (VC) 。

CoNDIS WAN 微型端口驱动程序在 NDIS **MaxSendWindow** \_ WAN \_ CO 信息结构的 MaxSendWindow 成员中指定它可以具有的未处理数据包的数量 \_ 。 当微型端口驱动程序从协议驱动程序响应 [OID \_ WAN \_ CO \_ GET \_ INFO](./oid-wan-co-get-info.md) 请求时，微型端口驱动程序会提供此结构。 但是，微型端口驱动程序可以通过使用[**WAN \_ CO \_ LINKPARAMS**](/previous-versions/windows/hardware/network/ff565819(v=vs.85))结构中的**SendWindow**成员，以动态方式和按 VC 调整此数字。 微型端口驱动程序将此结构传递给 [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) 函数。 NDISWAN 使用当前 **SendWindow** 值作为其未处理发送的限制。 微型端口驱动程序可以将 **SendWindow** 成员的值设置为零，以指定它无法处理任何未完成的数据包。 也就是说，如果 **SendWindow** 成员设置为零，则将关闭发送窗口，NDISWAN 停止发送特定 VC 的数据包。

如果设置了 PPP 组帧，则 WAN 微型端口驱动程序发送的数据包包含简单的 HDLC PPP 组帧。 对于 SLIP 或 RAS 组帧，数据包只包含无组帧的数据部分。 有关 WAN 数据包帧的详细信息，请参阅 [Wan 数据包组帧](wan-packet-framing.md)。

WAN 微型端口驱动程序不得尝试提供软件环回或混合模式环回。 NDISWAN 驱动程序完全支持这两种环回类型。

 

