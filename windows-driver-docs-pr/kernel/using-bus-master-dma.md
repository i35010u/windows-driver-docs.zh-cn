---
title: 使用总线主控 DMA
description: 使用总线主控 DMA
keywords:
- AdapterControl 例程，总线主控 DMA
- 总线主控 DMA WDK 内核
- DMA 传输 WDK 内核，总线主机 DMA
- 适配器对象 WDK 内核，主线-主 DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84b58f5c79605cd76b5e83dc05ccefe17e72a447
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825608"
---
# <a name="using-bus-master-dma"></a>使用总线主控 DMA





总线主控 DMA 设备的驱动程序可以使用以下类型的系统提供的 DMA 支持：

-   基于数据包的 DMA，如果总线主适配器允许驱动程序确定 DMA 传输操作的完成时间和/或何时开始另一个针对给定 IRP 的传输操作。 有关详细信息，请参阅 [使用 Packet-Based Bus-Master DMA](using-packet-based-bus-master-dma.md) 。

-   公共缓冲区 DMA (也称为 *连续 DMA*) 如果在总线主适配器为驱动程序提供了一种方法来确定传输操作将开始或传输完成的时间，或者如果是连续使用或重复使用单个缓冲区来进行 DMA 传输。 有关详细信息，请参阅 [使用 Common-Buffer Bus-Master DMA](using-common-buffer-bus-master-dma.md) 。

根据总线主适配器的性质，某些驱动程序只使用基于数据包的 DMA，某些驱动程序只使用公用缓冲区 DMA，一些使用这两者。 例如，使用邮箱方案传递状态信息和命令的总线主适配器驱动程序可能会将公用缓冲区用于驱动程序和其适配器之间共享的邮箱，同时还会将基于数据包的 DMA 用于数据传输。

 

 




