---
title: 公用缓冲区总线主控 DMA
description: 公用缓冲区总线主控 DMA
ms.assetid: 4758e084-1d9e-4e17-8627-05edc6b664ba
keywords:
- 主总线 DMA WDK 微型端口，常见的缓冲区
- DMA 总线 master WDK 微型端口，常见的缓冲区
- 常见缓冲区 DMA WDK 微型端口说明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392a2f1b98539f5f4136b836bede6c659c056943
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343021"
---
# <a name="common-buffer-bus-master-dma"></a>公用缓冲区总线主控 DMA


## <span id="ddk_common_buffer_bus_master_dma_gg"></span><span id="DDK_COMMON_BUFFER_BUS_MASTER_DMA_GG"></span>


微型端口驱动程序将执行以下一系列操作，使用常见缓冲区 DMA:

1.  获取适配器对象。

    微型端口驱动程序调用的视频端口驱动程序[ **VideoPortGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff570312)函数，通常在微型端口驱动程序[ *HwVidFindAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff567332)例程，以获取指向的指针[**副总裁\_DMA\_适配器**](https://msdn.microsoft.com/library/windows/hardware/ff570570)结构。 微型端口驱动程序将此指针用于后续 DMA 操作。

2.  分配常见的缓冲区。

    微型端口驱动程序调用的视频端口驱动程序[ **VideoPortAllocateCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff570178)函数，请使用上一步中获取的指针。

3.  释放常见的缓冲区。

    当微型端口驱动程序不再需要时常见的缓冲区时，它将调用的视频端口驱动程序[ **VideoPortReleaseCommonBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff570355)函数。

4.  放弃该适配器对象。

    此步骤可选。 如果由于某种原因，微型端口驱动程序决定将其剩余生存期内没有进一步 DMA 操作，应通过调用的视频端口驱动程序丢弃 DMA 适配器对象[ **VideoPortPutDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff570335)函数。

 

 





