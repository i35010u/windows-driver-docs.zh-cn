---
title: 拆分 ICMP 帧和其他上层协议帧
description: 拆分 ICMP 帧和其他上层协议帧
ms.assetid: 693c0b23-f9b5-4a1e-a6c7-5f658a9a636c
keywords:
- ICMP 帧拆分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b075000e83f42526b843d41a022a7beb1e4c9120
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562173"
---
# <a name="splitting-icmp-frames-and-other-upper-layer-protocol-frames"></a>拆分 ICMP 帧和其他上层协议帧





NIC 必须拆分 IP 上限层-协议而不是 TCP 或 UDP （例如，ICMP 帧） 上限层协议标头的开始处的帧，或必须不会拆分此类框架。

有关拆分的上限层协议标头的详细信息，请参阅[Upper 层协议标头的开始处拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

 

 





