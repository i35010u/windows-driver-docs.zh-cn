---
title: 在 TCP 有效负载中拆分帧
description: 在 TCP 有效负载中拆分帧
ms.assetid: 3d7c6f75-4523-4ad3-b15d-53f9d4ee1074
keywords:
- 以太网帧拆分 WDK 网络，TCP 有效负载
- TCP 有效负载 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c6d7ed911970817ce19848504744f151bc937fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392900"
---
# <a name="splitting-frames-at-the-tcp-payload"></a>在 TCP 有效负载中拆分帧





支持标头数据拆分的 NDIS 微型端口适配器必须支持 TCP 帧拆分帧的上限层协议标头。 但是，如果 TCP 标头不包含任何 TCP 选项，NIC 应拆分 TCP 有效负载的开头的帧。

NIC 可能不能拆分 TCP 帧，如果生成的标头缓冲区的长度大于最大标题大小更大长度。 当超过最大标头大小拆分帧的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

Nic 还必须支持拆分 TCP 标头与只有时间戳选项。 也就是说，时间戳选项为是必需的唯一 TCP 选项。 否则，对使用 TCP 选项的 TCP 标头的支持是可选的。 框架的 TCP 报头包含无法识别的 TCP 选项，如果 NIC 必须拆分 TCP 标头的开始处的帧 (即，upper 层协议标头) 或不会拆分帧。

**请注意**  标头数据要求，用于支持 IPv6 扩展标头或 TCP 选项的 IPv4 选项，即意味着要识别该元素，确定其长度，将其包含在标头 MDL 的 NIC 可以和在帧中找到其结束和下一个元素的开始。

 

有关拆分上限层协议标头的开始处的帧的详细信息，请参阅[Upper 层协议标头的开始处拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

如果标头数据拆分提供程序将拆分在 TCP 有效负载，所指示的帧[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构必须具有 NDIS\_NBL\_标志\_IS\_TCP 和 NDIS\_NBL\_标志\_拆分\_在\_上部\_层\_协议\_有效负载标记中的设置**NblFlags**成员。 有关详细信息，有关设置标头数据拆分 NET\_缓冲区\_标志列表，请参阅[设置 NET\_缓冲区\_列表信息](setting-net-buffer-list-information.md)。

 

 





