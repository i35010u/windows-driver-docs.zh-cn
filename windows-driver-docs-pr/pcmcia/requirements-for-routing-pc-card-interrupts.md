---
title: 路由电脑卡中断要求
description: 路由电脑卡中断要求
keywords:
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- 中断 WDK PCMCIA 总线
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da83990c04705ec2b66db1b84b27d87af9b18006
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806047"
---
# <a name="requirements-for-routing-pc-card-interrupts"></a>路由电脑卡中断要求





为了使用 PCI 中断而不是 ISA 中断，16位 PC 卡必须满足以下两个基本要求。

-   支持 PCI 级别触发的中断生成。 大多数16位 PC 卡符合此要求，因为 PCMCIA 标准指定 PC 卡和 CardBus 卡必须支持级别触发的中断。

-   支持中断共享。 许多16位 PC 卡不符合这一要求。 PCI 中断是可共享的，因此，如果智能卡不支持可共享中断，则系统无法向16位 PC 卡分配 PCI 中断号。 16位 PC 卡无法共享中断的常见原因包括：
    -   **中断服务例程 (ISR) 返回中断号失败。** 在 PCI 总线上，ISR 必须通过在中断完成后返回中断号来指示它正在处理哪个中断。 对于某些16位 PC 卡，Isr 不会执行此操作。
    -   **PC 卡出现故障，指示其在其硬件寄存器中断言的中断。** PC 卡必须在其硬件寄存器中指示其正在断言的中断的数量，以避免与其他设备的相同中断号争用。 某些16位 PC 卡不会执行此操作。
    -   **开机时产生虚假中断。** PC 卡不能生成由系统分配给它们的任何中断。 在系统分配中断之前，某些16位 PC 卡会生成虚假中断。

不满足这些要求的 PC 卡可能会导致中断风暴，导致引发系统崩溃。

 

 





