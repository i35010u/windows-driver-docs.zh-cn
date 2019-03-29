---
title: 拆分 IPv6 帧
description: 拆分 IPv6 帧
ms.assetid: fe18ccfb-29d0-4b57-9308-a9d4a9c6777a
keywords:
- 以太网帧拆分 WDK 网络 IPv6 帧
- IPv6 帧 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b58cea17046061a70be93a123b215b554ddaca7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569225"
---
# <a name="splitting-ipv6-frames"></a>拆分 IPv6 帧





若要支持标头数据拆分，但 NIC 必须支持拆分 IPv6 以太网帧，而无需任何 IPv6 扩展标头。 NIC 必须能拆分上限层协议标头的开始处的此类框架。

对 IPv6 以太网帧与 IPv6 扩展标头的支持是可选的。 NIC 可以支持 IPv6 的某些选项，不支持其他人。 NIC 必须不会拆分包含扩展标头的不支持的 IPv6 的 IPv6 帧。 拆分框架的标头部分必须包含整个 IPv6 标头和所有存在的 IPv6 扩展标头。

NIC 还可以支持标头数据拆分为碎片 IPv6 帧。 有关碎片 IPv4 帧的详细信息，请参阅[拆分碎片 IP 帧](splitting-fragmented-ip-frames.md)。

**请注意**  标头数据要求，用于支持 IPv6 扩展标头或 TCP 选项的 IPv4 选项，即意味着要识别该元素，确定其长度，将其包含在标头 MDL 的 NIC 可以和在帧中找到其结束和下一个元素的开始。

 

如果标头数据拆分为提供程序拆分 IPv6 帧，指示[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构必须具有 NDIS\_NBL\_标志\_IS\_中设置的 IPV6 标志**NblFlags**成员。 有关完整信息在 NET 中设置标头数据拆分标志\_缓冲区\_列表结构中，请参阅[设置 NET\_缓冲区\_列表信息](setting-net-buffer-list-information.md)。

其他以太网帧特性确定如何拆分 IPv6 帧。 如果含有碎片帧，请参阅[拆分碎片 IP 帧](splitting-fragmented-ip-frames.md)。 如果框架包含 TCP 信息，请参阅[拆分帧 TCP 有效负载](splitting-frames-at-the-tcp-payload.md)。 如果该框架包含 UDP 的信息，请参阅[UDP 负载拆分帧](splitting-frames-at-the-udp-payload.md)。 所有其他情况下，请参阅[拆分帧以外的其他 TCP 和 UDP](splitting-frames-other-than-tcp-and-udp.md)。

 

 





