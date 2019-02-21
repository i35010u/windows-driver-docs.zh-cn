---
title: PC 卡和卡驱动程序的设计最佳实践
description: PC 卡和卡驱动程序的设计最佳实践
ms.assetid: c3f31757-4063-4c68-ae19-1d8af98f81bc
keywords:
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线上，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- 中断 WDK PCMCIA 总线
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07762164ed7788d85650fa500e75be8e8ae38d5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545444"
---
# <a name="best-practices-for-the-design-of-pc-cards-and-card-drivers"></a>PC 卡和卡驱动程序的设计最佳实践





为了避免中断共享相关的问题，供应商和开发人员应遵守下列注意事项：

-   驱动程序开发人员应设计驱动程序以支持可共享 PCI 中断。

-   PC 卡制造商应该制造 CardBus 卡而不是 16 位 PC 卡，因为它们是遵守 PCI 标准。

-   所有的 16 位 PC 卡应支持可共享 PCI 中断。

-   所有 16 位 PC 卡应都支持连接到它们的设备的 I/O 资源的灵活的分配。 具体而言，卡应不会请求特定范围的 I/O 空间。 相反，它们应请求它们需要，并且允许系统功能，灵活地分配地址的 I/O 空间量。

-   计算机制造商应了解需要 ISA Irq 的设备，并且应确保 ISA 的 Irq 系统中是供 CardBus 控制器。

-   计算机制造商应确保 BIOS 代码将 CardBus 控制器设置为 PCIC 模式。

 

 





