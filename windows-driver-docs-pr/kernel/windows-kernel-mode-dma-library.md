---
title: Windows 内核模式 DMA 库
description: Windows 内核模式 DMA 库
ms.assetid: db6cc33a-474b-44a2-bd55-769ff31abae7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d0cb3fe82b615a0a10827021ac80e6929173bf90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358052"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows 内核模式 DMA 库


若要增强性能，设备可能需要直接访问的内存会绕过中央处理单元 (CPU) 的方式。 此技术称为直接内存访问 (DMA)。 Windows 设备驱动程序开发人员提供了一个 DMA 库。

驱动程序 DMA 的详细信息，请参阅[DMA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

DMA 例程的列表，请参阅[直接内存访问 (DMA) 库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

请注意，DMA 是用于设备和内存之间直接进行通信的技术，并且不与相同[设备的内存访问](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，这是一组宏提供用于读取和写入到 I/O 端口和 CPU 寄存器。

 

 




