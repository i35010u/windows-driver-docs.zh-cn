---
title: 拆分碎片化 IP 帧
description: 拆分碎片化 IP 帧
ms.assetid: faee7ec8-a49e-4107-a83f-d97391d69b43
keywords:
- 以太网帧拆分 WDK 网络、 碎片 IP 帧
- 碎片的 IP 帧 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8cb2b3c5cbe742aa30c0f4035dfe2a9234f5892
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369841"
---
# <a name="splitting-fragmented-ip-frames"></a>拆分碎片化 IP 帧





NIC 的碎片的 IP 帧包含 upper 层协议标头，如果必须拆分在帧[的右上层协议标头的开头](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)或必须不会拆分帧。 也就是说，NIC 必须不会拆分 TCP 或 UDP 负载的开始处的碎片的 IP 帧。

零碎的 IPv4 帧不包含上限层协议标头，如果 NIC 必须拆分 UDP 或 TCP 有效负载的开始处的帧，或必须不会拆分帧。

零碎的 IPv6 帧不包含上限层协议标头，如果 NIC 必须不会拆分帧。

有关拆分上限层协议标头的开始处的帧的详细信息，请参阅[Upper 层协议标头的开始处拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

 

 





