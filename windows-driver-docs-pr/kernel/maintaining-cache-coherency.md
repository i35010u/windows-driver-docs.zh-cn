---
title: 保持缓存一致性
description: 保持缓存一致性
ms.assetid: 70b4b313-ce33-4562-aa0d-127a91706409
keywords:
- I/O WDK 内核，缓存一致性
- 缓存协调性 WDK 内核
- 完整性 WDK I/O
- 数据传输 WDK 内核缓存一致性
- 传输数据 WDK 内核，缓存一致性
- 内存管理 WDK 内核缓存一致性
- 处理器缓存 WDK I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20495fec25a2aa119fe634e5ecb4852af180223d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378753"
---
# <a name="maintaining-cache-coherency"></a>保持缓存一致性


当驱动程序系统内存，并且其设备之间传输数据时，可以在一个或多个处理器缓存和/或系统 DMA 控制器的缓存中缓存数据。 驱动程序使用 DMA 或 PIO 到服务的读/写 Irp 或任何设备 I/O 控制请求都需要 DMA 或 PIO 数据传输操作应确保的完整性可能是缓存的数据在传输过程操作。 本部分介绍如何执行此操作。

本部分包含以下主题：

[正在刷新 DMA 操作期间缓存数据](flushing-cached-data-during-dma-operations.md)

[正在刷新 PIO 操作期间缓存数据](flushing-cached-data-during-pio-operations.md)

 

 




