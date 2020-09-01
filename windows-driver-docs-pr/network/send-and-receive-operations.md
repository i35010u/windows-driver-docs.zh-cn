---
title: 发送和接收操作
description: 发送和接收操作
ms.assetid: 216bfed2-92f8-4480-95fc-9909d7c1f533
keywords:
- 网络数据 WDK，发送
- 网络数据 WDK，接收
- 数据 WDK 网络，发送
- 数据 WDK 网络，接收
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- NET_BUFFER_LIST
- 多 NET_BUFFER_LIST 结构 WDK networki
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 285593231deac0b3ef6fd0d472b4c7cd80e8a694
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210077"
---
# <a name="send-and-receive-operations"></a>发送和接收操作





在单个函数调用中，NDIS 6.0 驱动程序可以在每个网络缓冲区列表结构上发送多个具有多个[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构 \_ \_ 。 此外，NDIS 驱动程序还可以针对 \_ \_ 网络缓冲区 \_ \_ 列表结构上具有多个网络缓冲区结构的多个网络缓冲区列表结构指示已完成的发送操作 \_ 。

在接收路径中，微型端口驱动程序可以使用网络 \_ 缓冲区 \_ 列表结构的列表来指示接收。 \_ \_ 微型端口驱动程序指示的每个网络缓冲区列表包含一个网络 \_ 缓冲区结构。 但是，本机802.11 驱动程序可以具有多个网络 \_ 缓冲区结构。 由于不同的协议绑定可以处理每个网络 \_ 缓冲区 \_ 列表结构，因此 NDIS 可以 \_ 独立地将每个网络缓冲区 \_ 列表结构返回给微型端口驱动程序。

支持 NDIS 5。*x* 及更早版本的驱动程序，ndis 在基于 [**NDIS \_ 数据包**](/previous-versions/windows/hardware/network/ff557086(v=vs.85))和基于网络缓冲区的接口之间提供转换层 \_ 。 NDIS 在 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构和 NDIS 数据包结构之间执行必要的转换 \_ 。 为了避免由于转换而导致性能下降，必须更新 NDIS 驱动程序以使用网络 \_ 缓冲区结构，并且应支持所有数据路径中的多个 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。

本节包括下列主题：

[发送网络数据](sending-network-data.md)

[取消发送操作](canceling-a-send-operation.md)

[接收网络数据](receiving-network-data.md)

[环回 NDIS 数据包](looping-back-ndis-packets.md)

 

