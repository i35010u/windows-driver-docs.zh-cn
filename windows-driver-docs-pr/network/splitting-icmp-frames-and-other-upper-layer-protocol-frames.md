---
title: 拆分 ICMP 帧和其他上层协议帧
description: 拆分 ICMP 帧和其他上层协议帧
keywords:
- ICMP 帧拆分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 093f00ebc52b8ef818cb4161e3d876d12c5ad7cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797881"
---
# <a name="splitting-icmp-frames-and-other-upper-layer-protocol-frames"></a>拆分 ICMP 帧和其他上层协议帧





NIC 必须用除 TCP 或 UDP 以外的上层协议来拆分 IP 帧 (例如，在上层协议标头的开头) 的 ICMP 帧，或者不得拆分此类帧。

有关在上层协议标头处拆分的详细信息，请参阅在 [上层协议标头的开头拆分帧](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)。

 

 





