---
title: 拆分 IPsec 帧
description: 拆分 IPsec 帧
keywords:
- 网络帧拆分 WDK 网络，IPsec 帧
- IPsec 帧拆分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d608f0865467f5c44f783e5644024b66bf5211
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797879"
---
# <a name="splitting-ipsec-frames"></a>拆分 IPsec 帧

\[IPsec 任务卸载功能已弃用，不应使用。\]




NIC 可以在 [上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)、 [TCP 负载的开头](splitting-frames-at-the-tcp-payload.md)或 [UDP 有效负载的开头](splitting-frames-at-the-udp-payload.md)拆分 IPsec 帧。 NIC 应将 IPsec 信息视为 IPv4 选项或 IPv6 扩展标头。

如果生成的标头缓冲区的长度大于最大标头大小，则 NIC 可能无法拆分此帧。 有关最大标头大小的详细信息，请参阅 [分配标头缓冲区](allocating-the-header-buffer.md)。

 

 





