---
title: 路由 PC 卡要求中断
description: 路由 PC 卡要求中断
ms.assetid: dbe01864-f05b-4004-9b04-bdefc5055e78
keywords:
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线上，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- 中断 WDK PCMCIA 总线
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 719f4e5ee45fb620b31031d1d0806c8c8cd5342b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554615"
---
# <a name="requirements-for-routing-pc-card-interrupts"></a>路由 PC 卡要求中断





若要使用而不是 ISA 中断 PCI 中断，16 位 PC 卡必须满足以下两个基本要求。

-   对 PCI 级别触发中断生成的支持。 最 16 位 PC 卡符合此要求，因为 PCMCIA 标准指定 PC 卡和 CardBus 卡必须支持级别触发中断。

-   中断共享的支持。 很多的 16 位 PC 卡不符合此要求。 PCI 中断都是可共享，因此如果卡不支持可共享中断系统不能将 PCI 中断号分配到 16 位 PC 卡。 16 位 PC 卡为什么不能共享中断的常见原因包括：
    -   **若要返回的中断数的中断服务例程 (ISR) 失败。** PCI 总线上 ISR 必须指示哪种中断它正在服务通过后返回的中断数完成。 对于某些 16 位 PC 卡 Isr 请执行此操作。
    -   **若要指示它在其硬件寄存器中断言的中断的 PC 卡失败。** PC 卡必须指示它其硬件中的断言的中断数寄存器，以避免争夺相同中断数与其他设备。 某些 16 位 PC 卡请执行此操作。
    -   **虚假中断通电时生成。** PC 卡必须生成而非由系统分配给他们的任何中断。 通电之前系统分配它们中断, 时，某些 16 位 PC 卡生成虚假的中断。

不满足这些要求 PC 卡可能会导致系统崩溃，从而促使中断 storm。

 

 





