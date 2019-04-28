---
title: 拆分 IPv4 帧
description: 拆分 IPv4 帧
ms.assetid: 1906dc31-7969-49da-adc4-8a174923d9d5
keywords:
- 以太网帧拆分 WDK 网络 IPv4 帧
- IPv4 帧 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf1b4a9bda438fa7ba75850bc9600b3a08a0201b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346059"
---
# <a name="splitting-ipv4-frames"></a>拆分 IPv4 帧





若要支持标头数据拆分，但 NIC 必须支持拆分 IPv4 以太网帧具有任何 IPv4 选项。 NIC 必须能拆分在这种帧[的右上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

支持为 IPv4 以太网帧使用 IPv4 的选项是可选的。 NIC 可以支持 IPv4 的一些选项和其他。 NIC 必须不会拆分包含无法识别的 IPv4 选项的 IPv4 帧。 拆分框架的标头部分必须包含整个 IPv4 标头和所有存在的 IPv4 选项。

NIC 还可以支持标头数据拆分为碎片 IPv4 帧。 有关碎片 IPv4 帧的详细信息，请参阅[拆分碎片 IP 帧](splitting-fragmented-ip-frames.md)。

**请注意**  标头数据要求，用于支持 IPv6 扩展标头或 TCP 选项的 IPv4 选项，即意味着要识别该元素，确定其长度，将其包含在标头 MDL 的 NIC 可以和在帧中找到其结束和下一个元素的开始。

 

如果标头数据拆分为提供程序拆分 IPv4 帧，指示[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构必须具有 NDIS\_NBL\_标志\_IS\_中设置 IPV4 标志**NblFlags**成员。 有关完整信息在 NET 中设置标头数据拆分标志\_缓冲区\_列表结构中，请参阅[设置 NET\_缓冲区\_列表信息](setting-net-buffer-list-information.md)。

其他以太网帧特性确定如何拆分 IPv4 帧。 如果含有碎片 IP 帧，请参阅[拆分碎片 IP 帧](splitting-fragmented-ip-frames.md)。 如果框架包含 TCP 信息，请参阅[拆分帧 TCP 有效负载](splitting-frames-at-the-tcp-payload.md)。 如果该框架包含 UDP 的信息，请参阅[UDP 负载拆分帧](splitting-frames-at-the-udp-payload.md)。 所有其他情况下，请参阅[拆分帧以外的其他 TCP 和 UDP](splitting-frames-other-than-tcp-and-udp.md)。

 

 





