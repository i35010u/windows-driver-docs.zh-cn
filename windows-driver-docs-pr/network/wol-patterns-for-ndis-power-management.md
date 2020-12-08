---
title: NDIS 电源管理的 WOL 模式
description: NDIS 电源管理的 WOL 模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28d9e054e13c37252e06c55bab0f333057c92465
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836197"
---
# <a name="wol-patterns-for-ndis-power-management"></a>NDIS 电源管理的 WOL 模式





从 NDIS 6.20 开始，LAN 唤醒 (WOL) 模式支持 *唤醒模式匹配* 方法。 此 WOL 方法可以最大程度地减少虚假唤醒事件，并确保计算机在需要时恢复运行状态。 用于 WOL 模式的接口标识基于数据包类型的特定模式 (例如，IPv4) 上的 TCP SYN 数据包。 特定模式提供可靠的模式匹配。

有两种类型的 WOL 模式：

<a href="" id="wol-packet-"></a>WOL 数据包   
一种数据包，其中的唤醒模式定义特定的数据包类型， (例如 IPv4 上的 TCP SYN) 。

<a href="" id="wol-bitmap-"></a>WOL 位图   
使用偏移和位图指定的 WOL 模式。

**注意**  Ndis 6.20 和更高版本的 NDIS 还支持 *幻数据包方法唤醒* 。 此方法独立于 *唤醒模式匹配* 方法。

 

从 NDIS 6.20 开始，多个协议驱动程序可以在网络适配器上设置 WOL 模式。 若要确保在请求的 WOL 模式数量高于网络适配器可支持的数目时设置正确的 WOL 模式集，协议驱动程序会为每个 WOL 模式分配优先级。 当由于网络适配器资源不足而导致 NDIS 无法添加新的高优先级 WOL 模式时，NDIS 可以删除较低优先级的模式。

有关管理 WOL 模式的详细信息，请参阅 [添加和删除 LAN 唤醒模式](adding-and-deleting-wake-on-lan-patterns.md)。

有关 NDIS 6.20 和更高版本中支持的 WOL 方法的详细信息，请参阅 [ndis 6.20 中的 Wol 方法](introduction-to-ndis-6-20.md)。

 

 





