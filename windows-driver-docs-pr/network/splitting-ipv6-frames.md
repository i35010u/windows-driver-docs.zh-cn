---
title: 拆分 IPv6 帧
description: 拆分 IPv6 帧
ms.assetid: fe18ccfb-29d0-4b57-9308-a9d4a9c6777a
keywords:
- 通过以太网帧拆分 WDK 网络，IPv6 帧
- IPv6 帧 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7527df846b70113243a764ded53ca42bbd153300
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841861"
---
# <a name="splitting-ipv6-frames"></a>拆分 IPv6 帧





若要支持标头数据拆分，NIC 必须支持不使用任何 IPv6 扩展标头拆分 IPv6 以太网帧。 NIC 必须能够在上层协议标头的开头拆分此类帧。

支持 ipv6 以太网帧的 IPv6 扩展标头是可选的。 NIC 可支持某些 IPv6 选项，而不支持其他的选项。 NIC 不得拆分包含不支持的 IPv6 扩展标头的 IPv6 帧。 拆分框架的标头部分必须包含整个 IPv6 标头和所有 IPv6 扩展标头。

NIC 还可以支持分段 IPv6 帧的标头数据拆分。 有关分段 IPv4 帧的详细信息，请参阅[拆分分段的 IP 帧](splitting-fragmented-ip-frames.md)。

**请注意**，  支持 IPv4 选项（一个 IPv6 扩展标头或 TCP 选项，用于标头数据要求），这意味着 NIC 识别元素的能力，确定其长度，将其包含在标头 MDL 中，并找到其端和帧中下一个元素的开头。

 

如果标头-数据拆分提供程序拆分 IPv6 帧，则指定的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构必须具有 NDIS\_NBL\_标志\_在**NblFlags**成员中设置\_IPv6 标志。 有关在 NET\_缓冲区\_列表结构中设置标头数据拆分标志的完整信息，请参阅[设置 net\_缓冲区\_列表信息](setting-net-buffer-list-information.md)。

其他以太网帧特征确定如何拆分 IPv6 帧。 如果帧有碎片，请参阅[拆分分段的 IP 帧](splitting-fragmented-ip-frames.md)。 如果帧包含 TCP 信息，请参阅[在 TCP 负载处拆分帧](splitting-frames-at-the-tcp-payload.md)。 如果帧包含 UDP 信息，请参阅[在 UDP 负载处拆分帧](splitting-frames-at-the-udp-payload.md)。 对于所有其他情况，请参阅[拆分除 TCP 和 UDP 以外的帧](splitting-frames-other-than-tcp-and-udp.md)。

 

 





