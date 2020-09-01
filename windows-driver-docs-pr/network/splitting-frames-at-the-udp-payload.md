---
title: 在 UDP 有效负载中拆分帧
description: 在 UDP 有效负载中拆分帧
ms.assetid: 10116077-89d2-4d07-9807-46b6281e9851
keywords:
- 用于拆分 WDK 网络、UDP 有效负载的以太网帧
- UDP 负载 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cbb9d0242dfa891fddba4ac149f7a7870f9fadd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213165"
---
# <a name="splitting-frames-at-the-udp-payload"></a>在 UDP 有效负载中拆分帧





支持标头数据拆分的 NDIS 微型端口适配器必须支持 UDP 帧的高层协议标头上的拆分帧。 但是，NIC 必须首先尝试将帧拆分为 UDP 有效负载的开头。

如果生成的标头缓冲区的长度大于最大标头大小，则 NIC 可能无法拆分 UDP 帧。 有关超出最大标头大小时拆分框架的详细信息，请参阅 [分配标头缓冲区](allocating-the-header-buffer.md)。

如果 NIC 无法拆分 UDP 有效负载中的帧，则 NIC 会将帧拆分为上层协议标头的开头，否则不应拆分该帧。 有关在上层协议标头开头拆分框架的详细信息，请参阅 [在上层协议标头的开头拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

如果标头-数据拆分提供程序在 UDP 负载处拆分帧，则指定的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构必须在 \_ \_ \_ NblFlags 成员中设置的 NBL 标志为 \_ udp，并将 ndis \_ NBL 标记拆分为在 \_ \_ \_ \_ \_ \_ \_ **NblFlags**成员中设置的上层协议有效负载标志。 有关设置标头数据拆分网络 \_ 缓冲区列表标志的详细信息 \_ ，请参阅 [设置网络 \_ 缓冲区 \_ 列表信息](setting-net-buffer-list-information.md)。

 

