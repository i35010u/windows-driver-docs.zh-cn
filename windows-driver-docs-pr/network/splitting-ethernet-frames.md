---
title: 拆分以太网帧
description: 拆分以太网帧
ms.assetid: 7b857dee-2805-4004-8f31-452f0cff0e0c
keywords:
- 标头数据拆分 WDK，拆分的以太网帧
- 拆分以太网帧
- 拆分 WDK 网络的以太网帧
- 以太网帧拆分 WDK 网络，有关以太网帧拆分
- 标头数据拆分提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a01768105452ea638e2a5250761d0ca4fdb4c6b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388104"
---
# <a name="splitting-ethernet-frames"></a>拆分以太网帧





本部分介绍将应用于标头数据拆分的提供程序，具体取决于提供程序将会进行拆分的以太网帧的类型的特定标头数据拆分要求。

**请注意**  阅读本主题中的常规要求后，可以使用随后的主题以了解每种类型的以太网帧的特定要求。 在前面主题中的要求上构建更高版本的主题。 例如，如果框架包含 IPv4 和 UDP 的信息，请务必阅读[拆分 IPv4 帧](splitting-ipv4-frames.md)并[拆分帧 UDP 负载](splitting-frames-at-the-udp-payload.md)主题。

 

如果标头数据拆分为提供程序拆分符合标头数据帧拆分要求中所指示[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构必须具有NDIS\_NBL\_标志\_HD\_中设置拆分标志**NblFlags**成员。 如果标头数据拆分提供程序不会不会拆分一个帧，必须用下列标志中清除指示帧**NblFlags** :

-   NDIS\_NBL\_FLAGS\_HD\_SPLIT

-   NDIS\_NBL\_FLAGS\_SPLIT\_AT\_UPPER\_LAYER\_PROTOCOL\_HEADER

-   NDIS\_NBL\_标志\_拆分\_处\_上部\_层\_协议\_有效负载

有关详细信息，有关设置标头数据拆分 NET\_缓冲区\_清单标记和其他接收指示要求，请参阅[标头数据拆分接收指示](receive-indications-with-header-data-split.md)。

有标头数据拆分提供程序可以在何处拆分接收的帧之外的标头数据拆分提供程序要求的情况。 在这些情况下，该提供程序应永远不会拆分 IP 标头、 IPv4 选项、 IPsec 标头、 IPv6 扩展标头或大写层协议标头，中间的以太网帧除非第一个 MDL 包含如 NDIS 为指定的至少多少字节预测先行大小。 有关预测先行大小的详细信息，请参阅[OID\_代\_当前\_预测先行](https://msdn.microsoft.com/library/windows/hardware/ff569574)。

本部分包括：

[拆分 IPv4 帧](splitting-ipv4-frames.md)

[拆分 IPv6 帧](splitting-ipv6-frames.md)

[拆分碎片 IP 帧](splitting-fragmented-ip-frames.md)

[拆分上限层协议标头的开始处的帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)

[拆分在 TCP 有效负载的帧](splitting-frames-at-the-tcp-payload.md)

[拆分的 UDP 负载帧](splitting-frames-at-the-udp-payload.md)

[拆分 TCP 和 UDP 以外的帧](splitting-frames-other-than-tcp-and-udp.md)

 

 





