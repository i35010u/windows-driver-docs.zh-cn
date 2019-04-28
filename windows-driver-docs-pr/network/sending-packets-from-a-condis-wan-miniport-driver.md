---
title: 从 CoNDIS WAN 微型端口驱动程序发送数据包
description: 从 CoNDIS WAN 微型端口驱动程序发送数据包
ms.assetid: 66c42e90-e0d9-47d1-9e6d-cadb511bcb7a
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络数据包发送
- 环回 WDK 网络
- 软件环回 WDK 的网络
- 混杂模式环回 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38b7cca58a4078077c91857a9d088c572c33cdc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346748"
---
# <a name="sending-packets-from-a-condis-wan-miniport-driver"></a>从 CoNDIS WAN 微型端口驱动程序发送数据包





上层驱动程序调用[ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)若要发送到基础的 CoNDIS WAN 微型端口驱动程序的列表中的网络数据包[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 NDISWAN 中间驱动程序将转发这些 NET\_缓冲区\_来自上层驱动程序的列表结构。 NDISWAN 会发送指标前重新打包结构。 NDISWAN 转发数据包中新的 NET\_缓冲区\_列表结构。

NDISWAN 中间驱动程序调用 NDIS 转发新 NET\_缓冲区\_列表结构 NDIS 调用 WAN 微型端口驱动程序[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)函数。

WAN 的 CoNDIS 微型端口驱动程序拥有这两个 NET\_缓冲区\_列表结构和关联的数据之前在发送完成。 微型端口驱动程序必须更高版本调用[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)完成发送请求。

完成调用并不一定表示的已传输网络 datahas;但是除了智能 Nic 的网络数据通常已传输。 但是不完成调用，指示微型端口驱动程序已准备好发布 NET 的所有权\_缓冲区\_列表结构。

之后的 CoNDIS WAN 微型端口驱动程序将收到 NET\_缓冲区\_列表结构，其中包含网络数据包，它应将数据包发送出活动的虚拟连接 (VC) 上。

CoNDIS WAN 的微型端口驱动程序指定它可以具有每个 VC 中的未完成数据包数**MaxSendWindow**成员的 NDIS\_WAN\_共同\_信息结构。 微型端口驱动程序微型端口驱动程序响应时提供此结构[OID\_WAN\_共同\_获取\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569818)从协议驱动程序的请求。 但是，微型端口驱动程序可以调整此数字动态并在每个 VC 的基础上使用**SendWindow**中的成员[ **WAN\_CO\_LINKPARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff565819)结构。 微型端口驱动程序将传递到此结构[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)函数。 NDISWAN 使用当前**SendWindow**与未完成发送其上限的值。 微型端口驱动程序可以设置的值**SendWindow**为零的成员才能指定它无法处理任何未完成的数据包。 也就是说，如果**SendWindow**成员设置为零，发送窗口关闭的情况下，NDISWAN 停止将数据包发送有关特定 VC。

如果设置 PPP 帧，WAN 微型端口驱动程序将发送的数据包包含简单 HDLC PPP 帧。 对于单或 RAS 组帧数据包包含仅说明，否则没有帧的数据部分。 有关 WAN 数据包分帧的详细信息，请参阅[WAN 数据包分帧](wan-packet-framing.md)。

WAN 微型端口驱动程序必须尝试提供软件环回或 promiscuous 模式环回。 这两种环回类型完全支持通过 NDISWAN 驱动程序。

 

 





