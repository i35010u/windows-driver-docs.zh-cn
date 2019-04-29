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
ms.openlocfilehash: 937dee14c371b241bfff8bcfd19333c6c4d9bef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390189"
---
# <a name="avstream-dma-services"></a>AVStream DMA 服务





若要开发使用直接内存访问 (DMA) AVStream 微型驱动程序，可以执行标准 DMA 直接在用户模式下捕获缓冲区或可实现常见缓冲区 DMA。

这两种方法需要您的驱动程序通过调用获取 DMA 适配器[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)。

 

 




