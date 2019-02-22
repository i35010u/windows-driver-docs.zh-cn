---
title: PCMCIA IRQ Windows XP 上的路由
description: PCMCIA IRQ Windows XP 上的路由
ms.assetid: 9b3501ce-c536-4ec7-bb01-c449d3900fee
keywords:
- PCIC 桥 WDK PCMCIA 总线
- PCI PCMCIA 桥接 WDK PCMCIA 总线
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线上，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- 路由 WDK PCMCIA 总线 ISA PCI 中断
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e5c5f072224b59eac99aad8c84f6483373cffb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525766"
---
# <a name="pcmcia-irq-routing-on-windows-xp"></a>PCMCIA IRQ Windows XP 上的路由





有两个类 PCMCIA 卡受 CardBus 控制器：

-   32 位符合 PCI 规范 CardBus

-   16 位 PC 卡，它基本上是 ISA 的设备

CardBus 卡类似 PCI 设备在大多数方面，包括它们定义和管理其中断的方式。 系统分配的 PCI 总线上的设备分配的编号范围从它们 IRQ 号。

但的 16 位 PC 卡体系结构是早于 PCI 总线，因此很多这些卡要求 ISA 中断数字。 为了适应在系统中，卡都无法为 ISA 中断请求 (IRQ) 数没有访问这些数据卡，CardBus 控制器体系结构，可以使用的一种称为"ISA PCI 中断路由。 支持此方法的控制器是能够分配到设计为使用 ISA 中断号的 16 位数据卡的 PCI 中断数。

本部分讨论 ISA PCI 中断路由和与不支持 ISA PCI 中断路由的 16 位卡相关的问题。

在 CardBus 控制器的发明之前, 的大多数系统使用 PCI PCMCIA 桥，称为"PCIC 桥"，若要连接到计算机的 16 位 PC 卡。 这些桥不支持 CardBus 卡，也不支持 ISA PCI 中断路由。 因此，在本部分中的信息不适用于 PCIC 桥。

 

 





