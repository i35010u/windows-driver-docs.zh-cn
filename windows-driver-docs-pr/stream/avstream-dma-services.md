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
ms.openlocfilehash: b306c6294911a4d943048d6784a7b4f7e6d00add
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840625"
---
# <a name="avstream-dma-services"></a>AVStream DMA 服务





若要开发使用直接内存访问（DMA）的 AVStream 微型驱动程序，你可以直接在用户模式捕获缓冲区中执行标准 DMA，或者可以实现通用缓冲区 DMA。

这两种方法都需要驱动程序通过调用[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)来获取 DMA 适配器。

 

 




