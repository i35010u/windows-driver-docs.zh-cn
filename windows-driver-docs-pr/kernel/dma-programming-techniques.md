---
title: DMA 编程技术
description: DMA 编程技术
ms.assetid: bdd8ffa4-8f09-41ed-b0f8-8edabbe65393
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da41db80c79a48b7c55f7621b749a869f3f8c676
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554183"
---
# <a name="dma-programming-techniques"></a>DMA 编程技术


直接内存访问 (DMA) 是一种最基本的硬件技术的中央处理器 (CPU) 和特定的设备之间传输基于内存的数据。 计算机系统使用 DMA 控制器是处理内存传输，从而允许执行其他操作的 CPU 的中间设备。

驱动程序可以使用 DMA 控制器直接传输基于内存的数据。 以下主题讨论 DMA 与 I/O 编程相关的问题。

驱动程序可以使用控制 DMA 的适配器对象。 有关适配器的对象的详细信息，请参阅[适配器对象和 DMA](adapter-objects-and-dma.md)。

当驱动程序系统内存，并且其设备之间传输数据时，可以在一个或多个处理器缓存和/或系统 DMA 控制器的缓存中缓存数据。 有关 DMA 和缓存的详细信息，请参阅[刷新缓存数据在 DMA 操作期间](flushing-cached-data-during-dma-operations.md)。

如果你需要在 DMA 将操作拆分为较小的区块，请参阅[拆分 DMA 传输请求](splitting-dma-transfer-requests.md)。

可从 Windows 8 开始 DMA 操作接口的版本 3。 有关此接口的详细信息，请参阅[DMA 操作接口的版本 3](version-3-of-the-dma-operations-interface.md)。

 

 




