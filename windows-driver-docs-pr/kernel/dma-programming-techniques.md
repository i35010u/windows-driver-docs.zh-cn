---
title: DMA 编程技术
description: DMA 编程技术
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 389d6222e6847c43d0905803085d3de7a235e1ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817717"
---
# <a name="dma-programming-techniques"></a>DMA 编程技术


 (DMA) 的直接内存访问是在中央处理器 (CPU) 和特定设备之间传输基于内存的数据的最基本硬件方法之一。 计算机系统使用 DMA 控制器，该控制器是处理内存传输的中间设备，允许 CPU 执行其他操作。

驱动程序可以使用 DMA 控制器直接传输基于内存的数据。 以下主题讨论了与 i/o 编程相关的 DMA 问题。

驱动程序可以使用适配器对象控制 DMA。 有关适配器对象的详细信息，请参阅 [适配器对象和 DMA](./introduction-to-adapter-objects.md)。

当驱动程序在系统内存与其设备之间传输数据时，可以将数据缓存在一个或多个处理器缓存中，或者缓存到系统 DMA 控制器的缓存中。 有关 DMA 和缓存的详细信息，请参阅 [在 Dma 操作期间刷新缓存的数据](flushing-cached-data-during-dma-operations.md)。

如果需要将 DMA 操作拆分为较小的区块，请参阅 [拆分 Dma 传输请求](splitting-dma-transfer-requests.md)。

从 Windows 8 开始，将提供 DMA 操作接口的第3版。 有关此接口的详细信息，请参阅 [DMA 操作接口的版本 3](version-3-of-the-dma-operations-interface.md)。

 

