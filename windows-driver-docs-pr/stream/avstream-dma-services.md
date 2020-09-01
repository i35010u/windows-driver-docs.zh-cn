---
title: AVStream DMA 服务
description: AVStream DMA 服务
ms.assetid: ba1c525b-26b0-4778-b58b-f4169cfb972e
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
ms.openlocfilehash: 9139f65bccdb35b5ad0ed7151b6b46d00cdee670
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186633"
---
# <a name="avstream-dma-services"></a>AVStream DMA 服务





若要开发 (DMA) 使用直接内存访问的 AVStream 微型驱动程序，可以直接将标准 DMA 写入用户模式捕获缓冲区，也可以实现常见的缓冲区 DMA。

这两种方法都需要驱动程序通过调用 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)来获取 DMA 适配器。

 

