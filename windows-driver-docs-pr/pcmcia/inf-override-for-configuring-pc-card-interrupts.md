---
title: 用于配置 PC 卡 INF 替代中断
description: 用于配置 PC 卡 INF 替代中断
ms.assetid: 90c951c4-0106-426a-b650-aeb93b893206
keywords:
- IRQ 路由 WDK PCMCIA 总线
- PCMCIA WDK 总线上，IRQ 路由
- PC 卡 WDK PCMCIA 总线
- 中断 WDK PCMCIA 总线
- PCI 中断 WDK PCMCIA 总线
- ISA 中断 WDK PCMCIA 总线
- INF 文件 WDK PCMCIA 总线
- PcmciaExclusiveIrq
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 920d44b4cde6e909d55bddc55a9af7d0dbd0bbd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554612"
---
# <a name="inf-override-for-configuring-pc-card-interrupts"></a>用于配置 PC 卡 INF 替代中断





如果操作系统将路由从 16 位 PC 卡不支持可共享 PCI 中断的中断，系统可能会停止工作。 若要避免这种情况发生，应指示卡不支持通过将 PcmciaExclusiveIrq 指令放置在卡的 INF 文件可共享的中断。

例如，假设您有调制解调器的驱动程序包含并未设计为支持中断共享中断服务例程 (ISR)。 你可以指示要分配固定的 ISA 中断到调制解调器通过将以下行添加到 AddReg 部分中的调制解调器 INF 文件中的操作系统：

`HKR,,PcmciaExclusiveIrq,0x00010001,1`

但请注意，一旦设备的 INF 文件中输入 PcmciaExclusiveIrq 指令，设备将无法与任何控制器或不具有访问为 ISA 中断的桥。

 

 





