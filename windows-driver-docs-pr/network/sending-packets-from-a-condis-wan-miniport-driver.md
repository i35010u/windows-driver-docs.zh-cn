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
ms.openlocfilehash: 07bbad0de67fd1413188334737aa73e1b882c8ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841957"
---
# <a name="sending-packets-from-a-condis-wan-miniport-driver"></a>从 CoNDIS WAN 微型端口驱动程序发送数据包





上层驱动程序调用[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists) ，将网络数据包发送到网络\_列表结构的网络[ **\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的列表。 NDISWAN 中间驱动程序将这些 NET\_BUFFER\_列表结构从上层驱动程序转发。 NDISWAN 在发送之前重新打包结构。 NDISWAN 将新的 NET\_缓冲区中的数据包转发\_列表结构。

NDISWAN 中间驱动程序调用 NDIS 以将新的 NET\_缓冲区\_列表结构中转发，NDIS 调用 WAN 微型端口驱动程序的[**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数。

CoNDIS WAN 微型端口驱动程序拥有 NET\_缓冲区\_列表结构和关联数据，直到发送完成。 小型端口驱动程序稍后必须调用[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete)来完成发送请求。

完成调用不一定表示网络 datahas 已传输;但除智能 Nic 外，网络数据通常已传输。 完成调用后，会指示微型端口驱动程序已准备好释放 NET\_缓冲区的所有权\_列表结构。

CoNDIS WAN 微型端口驱动程序接收到包含网络数据包\_列表结构的网络\_缓冲区后，应将数据包发送到活动虚拟连接（VC）。

CoNDIS WAN 微型端口驱动程序指定在 NDIS 的**MaxSendWindow**成员中，它可以具有的未处理数据包的数量，\_WAN\_CO\_信息结构。 当微型端口驱动程序响应[OID\_WAN\_CO\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wan-co-get-info)从协议驱动程序获取\_信息请求时，微型端口驱动程序将提供此结构。 但是，微型端口驱动程序可以通过使用[**WAN\_CO\_LINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565819(v=vs.85))结构中的**SendWindow**成员，以动态方式和按 VC 调整此数字。 微型端口驱动程序将此结构传递给[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)函数。 NDISWAN 使用当前**SendWindow**值作为其未处理发送的限制。 微型端口驱动程序可以将**SendWindow**成员的值设置为零，以指定它无法处理任何未完成的数据包。 也就是说，如果**SendWindow**成员设置为零，则将关闭发送窗口，NDISWAN 停止发送特定 VC 的数据包。

如果设置了 PPP 组帧，则 WAN 微型端口驱动程序发送的数据包包含简单的 HDLC PPP 组帧。 对于 SLIP 或 RAS 组帧，数据包只包含无组帧的数据部分。 有关 WAN 数据包帧的详细信息，请参阅[Wan 数据包组帧](wan-packet-framing.md)。

WAN 微型端口驱动程序不得尝试提供软件环回或混合模式环回。 NDISWAN 驱动程序完全支持这两种环回类型。

 

 





