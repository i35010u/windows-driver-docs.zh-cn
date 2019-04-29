---
title: NDIS 6.20 中的 WOL 方法
description: NDIS 6.20 中的 WOL 方法
ms.assetid: A46C213D-B356-44A3-8863-D7B183B73C77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8cd7dc9eb916b4ba5aaa10e816e7fd7616954f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379783"
---
# <a name="wol-methods-in-ndis-620"></a>NDIS 6.20 中的 WOL 方法





NDIS 6.20 和更高版本的 NDIS 中支持的电源管理功能包括以下 LAN 唤醒 (WOL) 方法：

-   项的幻数据包唤醒

-   唤醒模式匹配

-   在媒体上的唤醒设备连接

有关在以前版本的 Windows 电源管理功能的详细信息，请参阅[（NDIS 6.0 和更高版本） 的电源管理](https://msdn.microsoft.com/library/windows/hardware/hh205401)。

*上的幻数据包唤醒*方法中唤醒计算机时的网络适配器接收*幻数据包*。 一个*幻数据包*包含 16 个连续副本的接收网络适配器的以太网地址。

*上的幻数据包唤醒*方法是分开*唤醒模式匹配*方法。 WOL 模式包括其他的数据包类型或位图。 WOL 模式的详细信息，请参阅[NDIS 电源管理的 WOL 模式](wol-patterns-for-ndis-power-management.md)。

尽管某些网络适配器报告的支持*介质上的唤醒设备连接*方法中，以前版本的 Windows 没有。 完全支持 Windows 7*介质上的唤醒设备连接*方法如果 NDIS 6.20 微型端口驱动程序报告的支持。 NDIS 将网络适配器设置为低功耗状态，如果媒体已断开连接。

有关详细信息*介质上的唤醒设备连接*方法，请参阅[媒体断开连接的低开机](low-power-on-media-disconnect.md)。

 

 





