---
title: ISDN 和交换的 56k 摄影
description: ISDN 和交换的 56k 摄影
ms.assetid: e0532ded-c429-4f3a-b3c9-fd8ccc6b1b65
keywords:
- 数据包分帧 WDK WAN，ISDN 组帧
- ISDN 组帧 WDK WAN
- 数据包分帧 WDK WAN 切换组帧 56k
- 交换的 56k 组帧 WDK WAN
- WAN 数据包分帧 WDK 网络 ISDN 组帧
- WAN 数据包分帧网络交换 56k 分帧的 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3bf24405b5c50b20f7fd91d8231f4dc95974094
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542841"
---
# <a name="isdn-and-switched-56k-framing"></a>ISDN 和交换的 56k 摄影





最初，应使用 ISDN B 通道 （不 D 通道）。 多个 B 通道支持通过多链路 NDISWAN 的支持。 最初，应使用带 NRZ 编码位同步 HDLC 组帧。 应由驱动程序或 ISDN 硬件提供透明度。 它也是 ISDN 驱动程序或硬件为 NRZ 编码来计算 FCS 若要添加 PPP 结束标志 (0x7E)，并插入任何间帧时间填充提供的责任。 交换的 56k 驱动程序应帧 ISDN 的方式相同。

 

 





