---
title: 拆分以太网帧概述
description: 拆分以太网帧概述
ms.assetid: 7b857dee-2805-4004-8f31-452f0cff0e0c
keywords:
- 标头-数据拆分 WDK，以太网帧拆分
- 拆分以太网帧
- 拆分 WDK 网络的以太网帧
- 关于以太网帧拆分的以太网帧拆分 WDK 网络
- 标头-数据拆分提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c2d88d641b420daf73aff6457cba39df7246cb3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207193"
---
# <a name="splitting-ethernet-frames-overview"></a>拆分以太网帧概述

本部分介绍适用于标头数据拆分提供程序的特定标头数据拆分要求，具体取决于提供程序拆分的以太网帧的类型。

**注意**   阅读本主题中的常规要求后，可以使用后续主题来了解每种类型的以太网帧的特定要求。 后面的主题基于前面主题中的要求。 例如，如果一个帧包含 IPv4 和 UDP 信息，则应在 UDP 负载主题中阅读 [拆分 Ipv4 帧](splitting-ipv4-frames.md) 和 [拆分帧](splitting-frames-at-the-udp-payload.md) 部分。

 

如果标头-数据拆分提供程序根据标头-数据拆分要求拆分框架，则指定的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构必须 \_ \_ \_ \_ 在 **NblFlags** 成员中设置 NDIS NBL 标志 HD split 标志。 如果标头-数据拆分提供程序不拆分帧，则必须在 **NblFlags** 中清除以下标志：

-   NDIS \_ NBL \_ 标志 \_ HD \_ SPLIT

-   \_ \_ \_ \_ 在 \_ 上层 \_ \_ 协议 \_ 标头处拆分的 NDIS NBL 标志

-   \_ \_ \_ \_ 在 \_ 上层 \_ \_ 协议 \_ 有效负载处拆分的 NDIS NBL 标志

有关设置标头数据拆分网络 \_ 缓冲区 \_ 列表标志和其他接收指示要求的详细信息，请参阅 [带标头的接收指示-数据拆分](receive-indications-with-header-data-split.md)。

在某些情况下，标头-数据拆分提供程序可以将接收的帧拆分为标头-数据拆分提供程序要求之外。 在这些情况下，访问接口不应在 IP 标头、IPv4 选项、IPsec 标头、IPv6 扩展标头或上层协议标头中间拆分以太网帧，除非第一个 MDL 至少包含与为预测先行大小指定的 NDIS 相同的字节数。 有关预测先行大小的详细信息，请参阅 [OID \_ GEN \_ 当前 \_ 预测先行](./oid-gen-current-lookahead.md)。

本节包括：

[拆分 IPv4 帧](splitting-ipv4-frames.md)

[拆分 IPv6 帧](splitting-ipv6-frames.md)

[拆分碎片化 IP 帧](splitting-fragmented-ip-frames.md)

[在上层协议标头的开头拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)

[在 TCP 有效负载中拆分帧](splitting-frames-at-the-tcp-payload.md)

[在 UDP 有效负载中拆分帧](splitting-frames-at-the-udp-payload.md)

[拆分除 TCP 和 UDP 以外的帧](splitting-frames-other-than-tcp-and-udp.md)

 

