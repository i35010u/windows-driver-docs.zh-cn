---
title: 使用系统 DMA
description: 使用系统 DMA
ms.assetid: 8d478365-a6c8-4488-9f75-53a822d1daa2
keywords:
- AdapterControl 例程，系统 DMA
- 系统 DMA WDK 内核
- 适配器对象 WDK 内核，系统 DMA
- DMA 传输 WDK 内核，系统 DMA
- 从设备 WDK DMA
- 系统 DMA WDK 内核，有关系统 DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7984b4a9334648985cc8b3067545f21868b417a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379061"
---
# <a name="using-system-dma"></a>使用系统 DMA





从属 DMA 设备的驱动程序使用的系统提供 DMA 支持以下类型之一：

-   基于数据包的 DMA，如果该驱动程序不需要使用系统 DMA 控制器的自动初始化模式。 请参阅[使用基于数据包的系统 DMA](using-packet-based-system-dma.md)。

-   常见缓冲区 DMA，如果该驱动程序使用的自动初始化模式。 请参阅[使用常见缓冲区系统 DMA](using-common-buffer-system-dma.md)。

此外，任何驱动程序，使用基于数据包的 DMA 可以使用旨在简化支持例程散播-聚集 DMA，而不考虑其设备支持内置的分散/集中。 请参阅[使用散播-聚集 DMA](using-scatter-gather-dma.md)有关详细信息。

 

 




