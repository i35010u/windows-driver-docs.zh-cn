---
title: AVStream DMA 服务
description: AVStream DMA 服务
keywords:
- AVStream WDK，硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
- 捕获缓冲区 WDK AVStream
- 缓冲区 WDK AVStream
- AVStream DMA WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02690ad2291beb88503a04989079525b33df6dff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786655"
---
# <a name="avstream-dma-services"></a>AVStream DMA 服务





若要开发 (DMA) 使用直接内存访问的 AVStream 微型驱动程序，可以直接将标准 DMA 写入用户模式捕获缓冲区，也可以实现常见的缓冲区 DMA。

这两种方法都需要驱动程序通过调用 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)来获取 DMA 适配器。

 

