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
ms.openlocfilehash: 54e4cdf46502759da1b7d87bfd7f44179ba6e193
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841939"
---
# <a name="setting-net_buffer_list-information"></a>设置 NET\_缓冲区\_列表信息





标头-数据拆分提供程序必须将[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的**NblFlags**成员中的标头数据拆分标志设置为接收指示的\_列表结构。 对于拆分框架，NIC 还必须提供每个[**净\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的**DataPhysicalAddress**成员中接收帧的数据部分的物理地址。

**请注意**  微型端口驱动程序可以设置 NET\_缓冲区结构的**DataPhysicalAddress**成员，即使 net\_缓冲区不与拆分框架相关联。 在这种情况下， **DataPhysicalAddress**包含标头 MDL 的物理地址。

 

标头-数据拆分提供程序将**NblFlags**成员中的标志与按位 "或" 运算组合在一起。

标头-数据拆分提供程序可以设置以下标志，即使它不拆分框架：

<a href="" id="ndis-nbl-flags-is-ipv4"></a>NDIS\_NBL\_标志\_是\_IPV4  
[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的所有帧都是 IPv4 帧。 如果设置了此标志，则不能设置\_IPV6 标志\_的 NDIS\_NBL\_标志。

<a href="" id="ndis-nbl-flags-is-ipv6"></a>NDIS\_NBL\_标志\_是\_IPV6  
NET\_BUFFER\_列表中的所有帧都是 IPv6 帧。 如果设置了此标志，则不得设置 NBL\_标志\_\_的 NDIS\_。

<a href="" id="ndis-nbl-flags-is-tcp"></a>NDIS\_NBL\_标志\_是\_TCP  
NET\_BUFFER\_列表中的所有帧都是 TCP 帧。 如果设置了此标志，则不能\_UDP\_NBL\_标志\_为。 而 NDIS\_NBL\_FLAGS\_是\_IPV4 或 NDIS\_NBL\_\_\_必须设置 IPV6。

<a href="" id="ndis-nbl-flags-is-udp"></a>NDIS\_NBL\_标志\_是\_UDP  
[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的所有帧都是 UDP 帧。 如果设置了此标志，\_则不能设置 NBL\_标志\_的 NDIS\_。 而 NDIS\_NBL\_FLAGS\_是\_IPV4 或 NDIS\_NBL\_\_\_必须设置 IPV6。

任何 NDIS 驱动程序都可以设置上述标志来进行调试、测试或其他目的。 如果驱动程序设置这些标志，则值必须准确描述接收帧的内容。 建议设置这些标志。

标头-数据拆分提供程序可以设置以下标头数据拆分标志：

<a href="" id="ndis-nbl-flags-hd-split"></a>NDIS\_NBL\_标志\_HD\_SPLIT  
标头和数据将在与[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构关联的所有以太网帧中拆分。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-header"></a>NDIS\_NBL\_标志\_拆分\_\_\_\_\_  
NET\_BUFFER\_列表结构的所有帧都在[上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)处拆分。 如果设置此标志，则 NDIS\_NBL\_标志\_是\_IPV4 或 NDIS\_NBL\_\_\_必须设置 IPV6。 此外，NDIS\_NBL\_标志\_是\_TCP 或 NDIS\_NBL\_标志\_可以设置\_UDP。 而且，NDIS\_NBL\_标志\_拆分\_\_\_\_\_协议，则不能设置的。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-payload"></a>NDIS\_NBL\_标志\_拆分\_\_\_\_\_  
NET\_缓冲区中的所有帧\_列表结构在[TCP 有效](splitting-frames-at-the-tcp-payload.md)负载或[UDP 有效负载开始](splitting-frames-at-the-udp-payload.md)时被拆分。 如果设置此标志，则 NDIS\_NBL\_标志\_是\_IPV4 或 NDIS\_NBL\_\_\_必须设置 IPV6。 NDIS\_NBL\_FLAGS\_是\_TCP 或 NDIS\_\_\_\_标志，则必须设置 UDP。 此外，不能设置\_\_的\_标志\_拆分\_\_\_\_协议。

如果标头-数据拆分提供程序不拆分帧，则必须在**NblFlags**中清除以下标志：

-   NDIS\_NBL\_标志\_HD\_SPLIT

-   NDIS\_NBL\_标志\_拆分\_\_\_\_\_

-   NDIS\_NBL\_标志\_拆分\_\_\_\_\_

 

 





