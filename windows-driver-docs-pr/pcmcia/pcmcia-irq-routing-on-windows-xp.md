---
title: Windows XP 上的 PCMCIA IRQ 路由
description: Windows XP 上的 PCMCIA IRQ 路由
keywords:
- PCIC 桥接 WDK PCMCIA 总线
- PCI 到 PCMCIA 桥接 WDK PCMCIA 总线
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- ISA 到 PCI 中断路由 WDK PCMCIA 总线
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d13108f3b05c310bd6e879ea7d11844a4721f4cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812491"
---
# <a name="pcmcia-irq-routing-on-windows-xp"></a>Windows XP 上的 PCMCIA IRQ 路由





CardBus 控制器支持两类 PCMCIA 卡：

-   32位 PCI 兼容 CardBus

-   16位 PC 卡，它们基本上是 ISA 设备

在大多数情况下，CardBus 卡的行为类似于 PCI 设备，其中包括定义和管理中断的方式。 系统会根据分配给 PCI 总线上设备的数字范围，为其分配 IRQ 号。

但16位 PC 卡的体系结构比 PCI 总线更早，因此其中许多卡都需要 ISA 中断号。 为了使卡无法访问 ISA 中断请求 (IRQ) 号，CardBus 控制器体系结构使用一种称为 "ISA 到 PCI 中断路由" 的技术。 支持此技术的控制器能够将 PCI 中断号分配到设计为使用 ISA 中断号的16位卡。

本部分讨论了 ISA 到 PCI 中断路由，以及与不支持 ISA 到 PCI 中断路由的16位卡相关的问题。

在发明控制器之前，大多数系统使用 PCI 到 PCMCIA 桥（称为 "PCIC 桥"），以便将16位 PC 卡连接到计算机。 这些桥不支持 CardBus 卡，也不支持 ISA 到 PCI 中断路由。 因此，本部分中的信息不适用于 PCIC 桥。

 

 





