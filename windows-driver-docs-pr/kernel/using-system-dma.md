---
title: 使用系统 DMA
description: 使用系统 DMA
ms.assetid: 8d478365-a6c8-4488-9f75-53a822d1daa2
keywords:
- AdapterControl 例程，系统 DMA
- 系统 DMA WDK 内核
- 适配器对象 WDK 内核，系统 DMA
- DMA 传输 WDK 内核，系统 DMA
- 从属设备 WDK DMA
- 系统 DMA WDK 内核，关于系统 DMA
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4aad36f6266e25db69b5cac5e849293c3d1e94a
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681671"
---
# <a name="using-system-dma"></a>使用系统 DMA





从属 DMA 设备的驱动程序使用下列系统提供的 DMA 支持类型之一：

-   基于数据包的 DMA （如果驱动程序不需要使用系统 DMA 控制器的自动初始化模式）。 请参阅[使用基于数据包的系统 DMA](using-packet-based-system-dma.md)。

-   公用缓冲区 DMA （如果驱动程序使用自动初始化模式）。 请参阅[使用公用缓冲区系统 DMA](using-common-buffer-system-dma.md)。

此外，使用基于数据包的 DMA 的任何驱动程序都可以使用支持例程来简化散播/聚集 DMA，无论其设备是否支持内置的散播/聚集支持。 有关详细信息，请参阅[使用散点/集合 DMA](using-scatter-gather-dma.md) 。

 

 




