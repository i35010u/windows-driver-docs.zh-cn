---
title: 在 TCP 有效负载中拆分帧
description: 在 TCP 有效负载中拆分帧
ms.assetid: 3d7c6f75-4523-4ad3-b15d-53f9d4ee1074
keywords:
- 以太网帧拆分 WDK 网络，TCP 有效负载
- TCP 负载 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5d3a9467efcee35ab6b1300b4e3ca258424e039
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841865"
---
# <a name="splitting-frames-at-the-tcp-payload"></a>在 TCP 有效负载中拆分帧





支持标头数据拆分的 NDIS 微型端口适配器必须支持 TCP 帧的高层协议标头上的拆分帧。 但是，如果 TCP 标头不包含任何 TCP 选项，则 NIC 会将帧拆分为 TCP 有效负载的开头。

如果生成的标头缓冲区的长度大于最大标头大小，则 NIC 可能无法拆分 TCP 帧。 有关超出最大标头大小时拆分框架的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

Nic 还必须支持仅通过 timestamp 选项拆分 TCP 标头。 也就是说，timestamp 选项是必需的唯一 TCP 选项。 否则，支持 tcp 标头和 TCP 选项是可选的。 如果某个帧的 TCP 标头包含无法识别的 TCP 选项，则 NIC 必须将该帧拆分为 TCP 标头的开头（即，位于上层协议标头）或不拆分该帧。

**请注意**，  支持 IPv4 选项（一个 IPv6 扩展标头或 TCP 选项，用于标头数据要求），这意味着 NIC 识别元素的能力，确定其长度，将其包含在标头 MDL 中，并找到其端和帧中下一个元素的开头。

 

有关在上层协议标头开头拆分框架的详细信息，请参阅[在上层协议标头的开头拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

如果标头-数据拆分提供程序在 TCP 负载处拆分帧，则指示的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构必须具有 NDIS\_NBL\_标志\_\_\_\_\_\_\_\_\_\_ 有关设置标头-数据拆分 NET\_BUFFER\_列表标志的详细信息，请参阅[设置 NET\_BUFFER\_列表信息](setting-net-buffer-list-information.md)。

 

 





