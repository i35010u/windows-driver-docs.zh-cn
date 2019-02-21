---
title: 使用总线 Master DMA
description: 使用总线 Master DMA
ms.assetid: 08357a55-aec2-4454-923f-6daaf1583a25
keywords:
- AdapterControl 例程，总线 master DMA
- 主总线 DMA WDK 内核
- DMA 传输 WDK 内核，总线 master DMA
- 适配器对象 WDK 内核，总线 master DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f83451eeae3184bd7ef0438443ff3a92c95f8a1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541205"
---
# <a name="using-bus-master-dma"></a>使用总线 Master DMA





主总线 DMA 设备的驱动程序可以使用以下类型的系统提供 DMA 支持：

-   基于数据包如果主机总线适配器允许驱动程序以确定完成 DMA 传输操作和/或何时开始另一个用于给定 IRP 的传输操作的 DMA。 请参阅[Using Packet-Based 总线 Master DMA](using-packet-based-bus-master-dma.md)有关详细信息。

-   常见缓冲区 DMA (也称为*连续 DMA*) 如果主机总线适配器不提供驱动程序来传输操作中将开始时或当传输已完成，轻松地确定一种方法，或使用单个缓冲区区域连续或重复的 DMA 传输。 请参阅[使用常见缓冲区总线 Master DMA](using-common-buffer-bus-master-dma.md)有关详细信息。

根据主机总线适配器的性质，某些驱动程序以独占方式使用基于数据包的 DMA、 一些以独占方式，使用常见缓冲区 DMA 和一些同时使用。 例如，使用邮箱方案来进行通信的状态信息和命令可能对驱动程序和其适配器，以及基于数据包的 DMA 数据之间共享邮箱使用常见的缓冲区的主机总线适配器的驱动程序将传输。

 

 




