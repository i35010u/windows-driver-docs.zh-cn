---
title: Windows 内核模式 DMA 库
description: Windows 内核模式 DMA 库
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 331f0f745dd6426a2859afc9fb08f7a233adfd8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816611"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows 内核模式 DMA 库


若要提高性能，设备可能需要直接访问内存，这种方式会绕过中心处理单元 (CPU) 。 这种技术称为 (DMA) 的直接内存访问。 Windows 为设备驱动程序开发人员提供 DMA 库。

有关驱动程序 DMA 的详细信息，请参阅 [Dma 编程技术](dma-programming-techniques.md)。

有关 DMA 例程的列表，请参阅 [ (DMA) 库例程的直接内存访问](/windows-hardware/drivers/ddi/_kernel/#dma)。

请注意，DMA 是一种用于在设备和内存之间直接进行通信的技术，与 [设备内存访问](/windows-hardware/drivers/ddi/_kernel/#device-memory-access)不同，后者是一组提供的用于读取和写入 i/o 端口和 CPU 注册的宏。

 

