---
title: 设置 NET_BUFFER_LIST 信息
description: 设置 NET_BUFFER_LIST 信息
ms.assetid: 28f50ab4-043b-47bb-af70-e8c892288f21
keywords:
- NET_BUFFER_LIST
- 标头-数据拆分 WDK，NET_BUFFER_LIST
- 标志 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ff87cb8f240186ee494b6491c9300256d97431b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214442"
---
# <a name="setting-net_buffer_list-information"></a>设置网络 \_ 缓冲区 \_ 列表信息





标头-数据拆分提供程序必须在用于接收指示的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的**NblFlags**成员中设置标头数据拆分标志。 对于拆分框架，NIC 还必须在每个[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的**DataPhysicalAddress**成员中提供接收帧的数据部分的物理地址。

**注意**   微型端口驱动程序可以设置 NET buffer 结构的**DataPhysicalAddress**成员 \_ ，即使 net \_ 缓冲区与拆分框架无关。 在这种情况下， **DataPhysicalAddress** 包含标头 MDL 的物理地址。

 

标头-数据拆分提供程序将 **NblFlags** 成员中的标志与按位 "或" 运算组合在一起。

标头-数据拆分提供程序可以设置以下标志，即使它不拆分框架：

<a href="" id="ndis-nbl-flags-is-ipv4"></a>NDIS \_ NBL \_ 标志 \_ 是 \_ IPV4  
[**NET \_ BUFFER \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的所有帧都是 IPv4 帧。 如果设置了此标志，则 \_ 不得设置 NDIS NBL \_ 标志 \_ \_ 。

<a href="" id="ndis-nbl-flags-is-ipv6"></a>NDIS \_ NBL \_ 标志 \_ 为 \_ IPV6  
NET BUFFER 列表中的所有帧 \_ \_ 都是 IPv6 帧。 如果设置了此标志，则 \_ 不得设置 NDIS NBL \_ 标志 \_ \_ 。

<a href="" id="ndis-nbl-flags-is-tcp"></a>NDIS \_ NBL \_ 标志 \_ 为 \_ TCP  
NET BUFFER 列表中的所有帧 \_ \_ 都是 TCP 帧。 如果设置了此标志， \_ \_ \_ 则不得设置 "UDP NBL 标志" \_ 。 而 NDIS \_ NBL \_ 标志为 IPV4，则 \_ \_ \_ \_ 必须设置 NBL 标志 \_ 为 \_ IPV6。

<a href="" id="ndis-nbl-flags-is-udp"></a>NDIS \_ NBL \_ 标志 \_ 是 \_ UDP  
[**NET \_ BUFFER \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的所有帧都是 UDP 帧。 如果设置了此标志， \_ \_ \_ 则 \_ 不得设置 TCP NBL 标志。 而 NDIS \_ NBL \_ 标志为 IPV4，则 \_ \_ \_ \_ 必须设置 NBL 标志 \_ 为 \_ IPV6。

任何 NDIS 驱动程序都可以设置上述标志来进行调试、测试或其他目的。 如果驱动程序设置这些标志，则值必须准确描述接收帧的内容。 建议设置这些标志。

标头-数据拆分提供程序可以设置以下标头数据拆分标志：

<a href="" id="ndis-nbl-flags-hd-split"></a>NDIS \_ NBL \_ 标志 \_ HD \_ SPLIT  
标头和数据将在与 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构关联的所有以太网帧中拆分。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-header"></a>\_ \_ \_ \_ 在 \_ 上层 \_ \_ 协议 \_ 标头处拆分的 NDIS NBL 标志  
NET BUFFER 列表结构中的所有 \_ 帧 \_ 都在 [上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)处拆分。 如果设置此标志，则必须设置以下两个 \_ NBL \_ 标志： \_ \_ IPV4 或 ndis \_ NBL \_ 标记 \_ 为 \_ IPV6。 此外，NDIS \_ NBL \_ 标志 \_ 为 \_ TCP 或 ndis \_ NBL \_ 标志 \_ 为 \_ UDP。 不能 \_ \_ \_ \_ \_ 设置位于上层 \_ \_ 协议 \_ 有效负载的 NDIS NBL 标志拆分。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-payload"></a>\_ \_ \_ \_ 在 \_ 上层 \_ \_ 协议 \_ 有效负载处拆分的 NDIS NBL 标志  
NET BUFFER 列表结构中的所有 \_ 帧 \_ 都在 [TCP 有效](splitting-frames-at-the-tcp-payload.md) 负载或 [UDP 有效负载开始](splitting-frames-at-the-udp-payload.md)处拆分。 如果设置此标志，则必须设置以下两个 \_ NBL \_ 标志： \_ \_ IPV4 或 ndis \_ NBL \_ 标记 \_ 为 \_ IPV6。 \_ \_ \_ \_ 必须设置 NBL 或 ndis \_ NBL \_ 标志 \_ 为 "UDP" \_ 。 此外， \_ 不能 \_ \_ \_ \_ 设置位于上层 \_ \_ 协议 \_ 标头的 NDIS NBL 标志。

如果标头-数据拆分提供程序不拆分帧，则必须在 **NblFlags** 中清除以下标志：

-   NDIS \_ NBL \_ 标志 \_ HD \_ SPLIT

-   \_ \_ \_ \_ 在 \_ 上层 \_ \_ 协议 \_ 标头处拆分的 NDIS NBL 标志

-   \_ \_ \_ \_ 在 \_ 上层 \_ \_ 协议 \_ 有效负载处拆分的 NDIS NBL 标志

 

