---
title: 在 UDP 有效负载中拆分帧
description: 在 UDP 有效负载中拆分帧
ms.assetid: 10116077-89d2-4d07-9807-46b6281e9851
keywords:
- 以太网帧拆分 WDK 网络，UDP 有效负载
- UDP 负载 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 950e148c4279c58af75519c85e06f9d8290f6fe6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383614"
---
# <a name="splitting-frames-at-the-udp-payload"></a>在 UDP 有效负载中拆分帧





支持标头数据拆分的 NDIS 微型端口适配器必须支持 UDP 帧拆分帧的上限层协议标头。 但是，NIC 必须首先尝试拆分 UDP 负载的开始处的帧。

NIC 可能不能拆分 UDP 框架，如果生成的标头缓冲区的长度大于最大标题大小更大长度。 当超过最大标头大小拆分帧的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

如果 NIC 不能拆分的 UDP 负载在帧，NIC 应拆分上限层协议标头的开始处的帧，或不应拆分帧。 有关拆分上限层协议标头的开始处的帧的详细信息，请参阅[Upper 层协议标头的开始处拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

如果标头数据拆分提供程序将在所指示的 UDP 负载帧拆分[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构必须具有 NDIS\_NBL\_标志\_IS\_UDP 和 NDIS\_NBL\_标志\_拆分\_在\_上部\_层\_协议\_有效负载标记中的设置**NblFlags**成员。 有关详细信息，有关设置标头数据拆分 NET\_缓冲区\_标志列表，请参阅[设置 NET\_缓冲区\_列表信息](setting-net-buffer-list-information.md)。

 

 





