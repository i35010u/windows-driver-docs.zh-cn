---
title: 保持缓存一致性
description: 保持缓存一致性
keywords:
- I/o WDK 内核，缓存一致性
- 缓存一致性 WDK 内核
- 完整性 WDK i/o
- 数据传输 WDK 内核，缓存一致性
- 传输数据 WDK 内核，缓存一致性
- 内存管理 WDK 内核，缓存一致性
- 处理器缓存 WDK i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2c9a876c0cad525236f84829b7499370652920c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815071"
---
# <a name="maintaining-cache-coherency"></a>保持缓存一致性


当驱动程序在系统内存与其设备之间传输数据时，可以将数据缓存在一个或多个处理器缓存中，或者缓存到系统 DMA 控制器的缓存中。 使用 DMA 或 PIO 来服务读/写 Irp 的驱动程序或任何需要 DMA 或 PIO 数据传输操作的设备 i/o 控制请求应在传输操作过程中确保缓存数据的完整性。 本部分说明如何执行此操作。

本节包含下列主题：

[执行 DMA 操作期间刷新缓存数据](flushing-cached-data-during-dma-operations.md)

[执行 PIO 操作期间刷新缓存数据](flushing-cached-data-during-pio-operations.md)

 

 




