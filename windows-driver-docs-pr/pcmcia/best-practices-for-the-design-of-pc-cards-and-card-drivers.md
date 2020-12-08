---
title: 电脑卡和卡驱动程序的设计最佳做法
description: 电脑卡和卡驱动程序的设计最佳做法
keywords:
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- 中断 WDK PCMCIA 总线
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c41ee6831b3fe778a21d697bf2df1d160f7669dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812517"
---
# <a name="best-practices-for-the-design-of-pc-cards-and-card-drivers"></a>电脑卡和卡驱动程序的设计最佳做法





为了避免与中断共享相关的问题，供应商和开发人员应注意以下注意事项：

-   驱动程序开发人员应设计驱动程序以支持可共享的 PCI 中断。

-   PC 卡制造商应该制造 CardBus 卡，而不是16位 PC 卡，因为它们符合 PCI 标准。

-   所有16位 PC 卡都应支持可共享的 PCI 中断。

-   所有16位 PC 卡都应支持对连接到它们的设备的 i/o 资源进行灵活分配。 特别是，卡片不应请求特定范围的 i/o 空间。 相反，它们应该请求所需的 i/o 空间量，并使系统可以灵活地分配地址。

-   计算机制造商应该知道，设备需要 ISA Irq，并应确保 ISA Irq 可用于系统中的 CardBus 控制器。

-   计算机制造商应确保 BIOS 代码将 CardBus 控制器设置为 PCIC 模式。

 

 





