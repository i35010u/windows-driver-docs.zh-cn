---
title: 用于配置电脑卡中断的 INF 替代
description: 用于配置电脑卡中断的 INF 替代
keywords:
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- 中断 WDK PCMCIA 总线
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
- INF 文件 WDK PCMCIA 总线
- PcmciaExclusiveIrq
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e638b62e546c6497d1447dcdabdb15deeaa01e61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812501"
---
# <a name="inf-override-for-configuring-pc-card-interrupts"></a>用于配置电脑卡中断的 INF 替代





如果操作系统从不支持可共享 PCI 中断的16位 PC 卡路由中断，则系统可能会停止工作。 若要防止此情况发生，你应该通过在卡的 INF 文件中放置一个 PcmciaExclusiveIrq 指令来指示该卡不支持可共享的中断。

例如，假设你有一个调制解调器，其驱动程序包含 (ISR) 的中断服务例程，而该服务不支持中断共享。 可以通过将以下行添加到调制解调器的 INF 文件中的 AddReg 部分，指导操作系统将固定的 ISA 中断分配到调制解调器：

`HKR,,PcmciaExclusiveIrq,0x00010001,1`

但请注意，一旦将 PcmciaExclusiveIrq 指令放入设备的 INF 文件中，该设备将无法与任何无法访问 ISA 中断的控制器或桥一起工作。

 

 





