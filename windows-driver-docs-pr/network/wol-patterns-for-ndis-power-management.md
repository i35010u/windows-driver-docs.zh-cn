---
title: NDIS 电源管理的 WOL 模式
description: NDIS 电源管理的 WOL 模式
ms.assetid: 44d49fe9-0983-4753-8f6f-f3445b5b9f3b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d769b7f8d0ca87df47368153100f015367a6a49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348619"
---
# <a name="wol-patterns-for-ndis-power-management"></a>NDIS 电源管理的 WOL 模式





从 NDIS 6.20 开始，对于支持 LAN 唤醒 (WOL) 模式*唤醒模式匹配*方法。 此 WOL 方法最大程度减少虚假唤醒事件，并确保，计算机将恢复到运行时预期的状态。 WOL 模式接口标识基于数据包类型 （例如，在 IPv4 TCP SYN 数据包） 的特定模式。 特定模式提供可靠的模式匹配。

有两种类型的 WOL 模式：

<a href="" id="wol-packet-"></a>WOL 数据包   
在其中唤醒模式定义特定的数据包类型 （如 IPv4 上的 TCP SYN) 数据包。

<a href="" id="wol-bitmap-"></a>WOL 位图   
具有偏移量和位图指定 WOL 模式。

**请注意**  NDIS 6.20 和更高版本的 NDIS 还支持*上的幻数据包唤醒*方法。 此方法是分开*唤醒模式匹配*方法。

 

从 NDIS 6.20 开始，多个协议驱动程序可以在网络适配器上设置 WOL 模式。 若要确保请求 WOL 模式数量高于网络适配器可以支持的数字时，设置一组正确的 WOL 模式，协议驱动程序分配到每个 WOL 模式的优先级。 NDIS 无法添加新的高优先级 WOL 模式，因为网络适配器的资源不足，NDIS 可以删除较低的优先级模式。

有关管理 WOL 模式的详细信息，请参阅[添加和删除唤醒 LAN 模式](adding-and-deleting-wake-on-lan-patterns.md)。

有关 NDIS 6.20 和更高版本中受支持的 WOL 方法的详细信息，请参阅[WOL 方法在 NDIS 6.20](introduction-to-ndis-6-20.md)。

 

 





