---
title: ISDN 和交换式 56K 分帧
description: ISDN 和交换式 56K 分帧
keywords:
- 数据包帧 WDK WAN，ISDN 组帧
- ISDN 帧 WDK WAN
- 数据包帧 WDK WAN，交换的56K 帧
- 交换的56K 帧式 WDK WAN
- WAN 数据包组帧 WDK 网络，ISDN 组帧
- WAN 数据包帧式 WDK 网络，切换56K 帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fa8738b6400352ef35b64c9de017c9d2bb32693
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789753"
---
# <a name="isdn-and-switched-56k-framing"></a>ISDN 和交换式 56K 分帧





最初，ISDN B 通道 (不应使用 D 通道) 。 多个 B 通道支持通过 NDISWAN 的多链路支持完成。 最初，应使用具有 NRZ 编码的位同步 HDLC 帧。 透明度应由驱动程序或 ISDN 硬件提供。 ISDN 驱动程序或硬件还负责提供 NRZ 编码，以便计算用来将 PPP 结束标志添加到 (0x7E) ，并插入任何帧间时间填充。 交换的56K 驱动程序应采用与 ISDN 相同的方式。

 

 





