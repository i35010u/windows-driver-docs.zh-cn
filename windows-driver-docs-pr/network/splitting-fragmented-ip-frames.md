---
title: 拆分碎片化 IP 帧
description: 拆分碎片化 IP 帧
keywords:
- 网络帧拆分 WDK 网络，分段 IP 帧
- 分段 IP 帧 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2540437c3c0b5d677265d5b4972ab4c19b36da83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797909"
---
# <a name="splitting-fragmented-ip-frames"></a>拆分碎片化 IP 帧





如果分段 IP 帧包含上层协议标头，则 NIC 必须在 [上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md) 拆分该帧，或者不得拆分该帧。 也就是说，NIC 不能在 TCP 或 UDP 有效负载的开头拆分分段 IP 帧。

如果零碎的 IPv4 帧不包含上层协议标头，则 NIC 必须在 UDP 或 TCP 负载开始时拆分该帧，否则不能拆分帧。

如果零碎的 IPv6 帧不包含上层协议标头，则 NIC 不得拆分此帧。

有关在上层协议标头开头拆分框架的详细信息，请参阅 [在上层协议标头的开头拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

 

 





