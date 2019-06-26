---
title: 设置 NET_BUFFER_LIST 信息
description: 设置 NET_BUFFER_LIST 信息
ms.assetid: 28f50ab4-043b-47bb-af70-e8c892288f21
keywords:
- NET_BUFFER_LIST
- 标头数据拆分 WDK，NET_BUFFER_LIST
- 标志 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a211b1f979f5bab2abec5f982c75a91f20a56bbc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377017"
---
# <a name="setting-netbufferlist-information"></a>设置 NET\_缓冲区\_列出信息





标头数据拆分提供程序必须标头数据拆分标志中设置**NblFlags**的成员[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构对于收到的指示。 对于拆分帧，NIC 还必须提供接收的帧中的数据部分的物理地址**DataPhysicalAddress**的每个成员[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。

**请注意**  微型端口驱动程序可以设置**DataPhysicalAddress** NET 成员\_缓冲区结构，即使 NET\_缓冲区不是与拆分框架相关联。 在这种情况下， **DataPhysicalAddress**包含标头 MDL 的物理地址。

 

标头数据拆分提供程序结合了中的标志**NblFlags**与按位或运算的成员。

即使将一个框架不拆分，标头数据拆分提供程序可以设置以下标志：

<a href="" id="ndis-nbl-flags-is-ipv4"></a>NDIS\_NBL\_FLAGS\_IS\_IPV4  
中的框架的所有[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) IPv4 帧。 如果设置此标志，NDIS\_NBL\_标志\_IS\_IPV6 标志不能设置。

<a href="" id="ndis-nbl-flags-is-ipv6"></a>NDIS\_NBL\_FLAGS\_IS\_IPV6  
所有在 NET 帧\_缓冲区\_列表是 IPv6 的帧。 如果设置此标志，NDIS\_NBL\_标志\_IS\_IPV4 标志不能设置。

<a href="" id="ndis-nbl-flags-is-tcp"></a>NDIS\_NBL\_FLAGS\_IS\_TCP  
所有在 NET 帧\_缓冲区\_列表是 TCP 帧。 如果设置此标志，NDIS\_NBL\_标志\_IS\_UDP 不能设置。 和任一 NDIS\_NBL\_标志\_IS\_IPV4 或 NDIS\_NBL\_标志\_IS\_必须设置 IPV6。

<a href="" id="ndis-nbl-flags-is-udp"></a>NDIS\_NBL\_FLAGS\_IS\_UDP  
中的框架的所有[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) UDP 帧。 如果设置此标志，NDIS\_NBL\_标志\_IS\_不能设置 TCP。 和任一 NDIS\_NBL\_标志\_IS\_IPV4 或 NDIS\_NBL\_标志\_IS\_必须设置 IPV6。

任何 NDIS 驱动程序可以设置用于调试、 测试或其他目的前面的标志。 如果驱动程序将这些标志，则值必须准确地描述接收的帧的内容。 建议设置这些标志。

标头数据拆分提供程序可以设置以下标头数据拆分标志：

<a href="" id="ndis-nbl-flags-hd-split"></a>NDIS\_NBL\_FLAGS\_HD\_SPLIT  
在所有与之关联的以太网帧中拆分的标头和数据[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-header"></a>NDIS\_NBL\_标志\_拆分\_处\_上部\_层\_协议\_标头  
所有在 NET 帧\_缓冲区\_列表结构拆分在[upper 层协议标头的开始](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。 如果设置此标志，任一 NDIS\_NBL\_标志\_IS\_IPV4 或 NDIS\_NBL\_标志\_IS\_必须设置 IPV6。 此外，任一 NDIS\_NBL\_标志\_IS\_TCP 或 NDIS\_NBL\_标志\_IS\_可以设置 UDP。 和 NDIS\_NBL\_标志\_拆分\_处\_上部\_层\_协议\_有效负载不能设置。

<a href="" id="ndis-nbl-flags-split-at-upper-layer-protocol-payload"></a>NDIS\_NBL\_标志\_拆分\_处\_上部\_层\_协议\_有效负载  
所有网络中的框架\_缓冲区\_列表结构拆分处[的 TCP 有效负载的开头](splitting-frames-at-the-tcp-payload.md)或[的 UDP 负载的开头](splitting-frames-at-the-udp-payload.md)。 如果设置此标志，任一 NDIS\_NBL\_标志\_IS\_IPV4 或 NDIS\_NBL\_标志\_IS\_必须设置 IPV6。 任一 NDIS\_NBL\_标志\_IS\_TCP 或 NDIS\_NBL\_标志\_IS\_必须设置 UDP。 此外，NDIS\_NBL\_标志\_拆分\_处\_上部\_层\_协议\_标头不能设置。

如果标头数据拆分提供程序不会不会拆分一个帧，必须用下列标志中清除指示帧**NblFlags** :

-   NDIS\_NBL\_FLAGS\_HD\_SPLIT

-   NDIS\_NBL\_FLAGS\_SPLIT\_AT\_UPPER\_LAYER\_PROTOCOL\_HEADER

-   NDIS\_NBL\_标志\_拆分\_处\_上部\_层\_协议\_有效负载

 

 





