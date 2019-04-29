---
title: 拆分 IPsec 帧
description: 拆分 IPsec 帧
ms.assetid: 2d6841f2-6eb6-4c59-80fb-5c777fa2bf56
keywords:
- 以太网帧拆分 WDK 网络，IPsec 帧
- IPsec 帧拆分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8eb1da0a1a376ba1884d14c2f919449dd9f4b22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392898"
---
# <a name="splitting-ipsec-frames"></a>拆分 IPsec 帧

\[IPsec 任务卸载功能已弃用，不应使用。\]




NIC 可以拆分 IPsec 帧[的右上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)，则[的 TCP 有效负载的开头](splitting-frames-at-the-tcp-payload.md)，或[的 UDP 负载的开头](splitting-frames-at-the-udp-payload.md)。 NIC 应视为 IPsec 信息相同选项 IPv4 或 IPv6 扩展标头。

NIC 可能不能将框架拆分如果生成的标头缓冲区的长度大于最大标题大小更大长度。 有关最大标头大小的详细信息，请参阅[分配标头缓冲区](allocating-the-header-buffer.md)。

 

 





