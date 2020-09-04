---
title: Windows 内核模式 DMA 库
description: Windows 内核模式 DMA 库
ms.assetid: db6cc33a-474b-44a2-bd55-769ff31abae7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f5b3907be82bacb7950482b7ba43036fa0ab2892
ms.sourcegitcommit: 6f9087dab3bf214c287b179829e6a59d74db0591
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89471906"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows 内核模式 DMA 库


若要提高性能，设备可能需要直接访问内存，这种方式会绕过中心处理单元 (CPU) 。 这种技术称为 (DMA) 的直接内存访问。 Windows 为设备驱动程序开发人员提供 DMA 库。

有关驱动程序 DMA 的详细信息，请参阅 [Dma 编程技术](dma-programming-techniques.md)。

有关 DMA 例程的列表，请参阅 [ (DMA) 库例程的直接内存访问](/windows-hardware/drivers/ddi/_kernel/#dma)。

请注意，DMA 是一种用于在设备和内存之间直接进行通信的技术，与 [设备内存访问](/windows-hardware/drivers/ddi/_kernel/#device-memory-access)不同，后者是一组提供的用于读取和写入 i/o 端口和 CPU 注册的宏。

 

