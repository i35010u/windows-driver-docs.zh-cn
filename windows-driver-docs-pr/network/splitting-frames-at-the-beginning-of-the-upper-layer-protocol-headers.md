---
title: 正在开始拆分高层协议标头中的帧
description: 在上端 Layer-Protocol 标头的开头拆分帧
keywords:
- 从上层协议开头拆分了 "WDK 网络" 的以太网帧
- 上层协议 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56d4d5dcbd9622d78d58ff883d5e9e1970987e41
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249136"
---
# <a name="splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers"></a>在上端 Layer-Protocol 标头的开头拆分帧





*上层协议* 是 IP 传输协议，例如 TCP、UDP 或 ICMP。

**注意**  在标头中，IPsec 不被视为数据拆分要求的上层协议。 有关拆分 IPsec 帧的详细信息，请参阅 [拆分 Ipsec 帧](splitting-ipsec-frames.md)。

 

如果 NIC 在上层协议标头的开头拆分了以太网帧，则指定的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 必须正好包含两个 MDLs。 第一个 MDL 描述的缓冲区必须以 (MAC 标头的以太网帧的第一个字节开头) 并且第二个 MDL 描述的缓冲区必须从上层协议标头的第一个字节开始。

**注意**  NIC 可以在 TCP 或 UDP 有效负载处拆分 TCP 和 UDP 帧。 有关详细信息，请参阅在 [TCP 负载处拆分帧](splitting-frames-at-the-tcp-payload.md) 和 [在 UDP 负载处拆分帧](splitting-frames-at-the-udp-payload.md)。

 

如果标头-数据拆分提供程序在上层协议标头的开头拆分该帧，则指定的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构必须在 \_ \_ \_ \_ \_ \_ \_ \_ **NBLFLAGS** 成员中设置的上层协议标头标志处拆分 NDIS NBL 标志。 有关设置标头数据拆分网络 \_ 缓冲区列表标志的详细信息 \_ ，请参阅 [设置网络 \_ 缓冲区 \_ 列表信息](setting-net-buffer-list-information.md)。

如果生成的标头缓冲区的长度大于最大标头大小，则 NIC 不得拆分帧。 有关超出最大标头大小时拆分框架的详细信息，请参阅 [分配标头缓冲区](allocating-the-header-buffer.md)。

 

