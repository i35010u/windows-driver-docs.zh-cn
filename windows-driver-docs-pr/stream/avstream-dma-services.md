---
title: AVStream DMA 服务
description: AVStream DMA 服务
ms.assetid: ba1c525b-26b0-4778-b58b-f4169cfb972e
keywords:
- AVStream WDK 硬件
- 硬件 WDK AVStream
- DMA 服务 WDK AVStream
- 直接内存访问 WDK AVStream
- 捕获缓冲区 WDK AVStream
- 缓冲区 WDK AVStream
- AVStream DMA WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d16c18fb65ac3e735f0965bdaf632f753a53263
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386693"
---
# <a name="avstream-dma-services"></a>AVStream DMA 服务





若要开发使用直接内存访问 (DMA) AVStream 微型驱动程序，可以执行标准 DMA 直接在用户模式下捕获缓冲区或可实现常见缓冲区 DMA。

这两种方法需要您的驱动程序通过调用获取 DMA 适配器[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)。

 

 




