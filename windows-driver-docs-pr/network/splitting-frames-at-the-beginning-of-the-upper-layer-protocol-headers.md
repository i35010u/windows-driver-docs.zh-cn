---
title: 正在开始拆分高层协议标头中的帧
description: 在上层协议标头的开头拆分帧
ms.assetid: 2559ac20-46dc-4116-9d12-b2cd634e501b
keywords:
- 从上层协议开头拆分了 "WDK 网络" 的以太网帧
- 上层协议 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ac667525619b94bd67b5e6b6a653d2c4073edfa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841869"
---
# <a name="splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers"></a>在上层协议标头的开头拆分帧





*上层协议*是 IP 传输协议，例如 TCP、UDP 或 ICMP。

**请注意**  IPsec 不会被视为标头数据拆分要求中的上层协议。 有关拆分 IPsec 帧的详细信息，请参阅[拆分 Ipsec 帧](splitting-ipsec-frames.md)。

 

如果 NIC 在上层协议标头的开头拆分了以太网帧，则指示的[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)必须正好包含两个 MDLs。 第一种 MDL 描述的缓冲区必须以以太网帧（MAC 标头）的第一个字节开头，第二个 MDL 描述的缓冲区必须从上层协议标头的第一个字节开始。

**请注意**，在 TCP 或 udp 有效负载下，NIC 可以拆分 TCP 和 udp 帧  。 有关详细信息，请参阅在[TCP 负载处拆分帧](splitting-frames-at-the-tcp-payload.md)和[在 UDP 负载处拆分帧](splitting-frames-at-the-udp-payload.md)。

 

如果标头-数据拆分提供程序拆分位于上层协议标头开头的帧，则指示的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构必须具有 NDIS\_NBL\_标志\_在\_拆分\_\_层\_在**NblFlags**成员中设置的协议\_标头标志。 有关设置标头-数据拆分 NET\_BUFFER\_列表标志的详细信息，请参阅[设置 NET\_BUFFER\_列表信息](setting-net-buffer-list-information.md)。

如果生成的标头缓冲区的长度大于最大标头大小，则 NIC 不得拆分帧。 有关超出最大标头大小时拆分框架的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

 

 





