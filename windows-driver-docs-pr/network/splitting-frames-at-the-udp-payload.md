---
title: 在 UDP 有效负载中拆分帧
description: 在 UDP 有效负载中拆分帧
ms.assetid: 10116077-89d2-4d07-9807-46b6281e9851
keywords:
- 用于拆分 WDK 网络、UDP 有效负载的以太网帧
- UDP 负载 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a72cd08e833641f95e76db34205fb6cbe20bf50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841863"
---
# <a name="splitting-frames-at-the-udp-payload"></a>在 UDP 有效负载中拆分帧





支持标头数据拆分的 NDIS 微型端口适配器必须支持 UDP 帧的高层协议标头上的拆分帧。 但是，NIC 必须首先尝试将帧拆分为 UDP 有效负载的开头。

如果生成的标头缓冲区的长度大于最大标头大小，则 NIC 可能无法拆分 UDP 帧。 有关超出最大标头大小时拆分框架的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

如果 NIC 无法拆分 UDP 有效负载中的帧，则 NIC 会将帧拆分为上层协议标头的开头，否则不应拆分该帧。 有关在上层协议标头开头拆分框架的详细信息，请参阅[在上层协议标头的开头拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

如果标头-数据拆分提供程序在 UDP 负载处拆分了帧，则指定的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构必须具有 NDIS\_NBL\_标志\_\_UDP，NDIS\_NBL\_标志\_在**NblFlags**成员中设置\_协议\_负载标志的\_层\_上，拆分\_。 有关设置标头-数据拆分 NET\_BUFFER\_列表标志的详细信息，请参阅[设置 NET\_BUFFER\_列表信息](setting-net-buffer-list-information.md)。

 

 





