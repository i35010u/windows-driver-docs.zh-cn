---
title: Windows 内核模式 DMA 库
description: Windows 内核模式 DMA 库
ms.assetid: db6cc33a-474b-44a2-bd55-769ff31abae7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4679032d823e128628071ace53f635c877c3fe1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383184"
---
# <a name="windows-kernel-mode-dma-library"></a>Windows 内核模式 DMA 库


若要增强性能，设备可能需要直接访问的内存会绕过中央处理单元 (CPU) 的方式。 此技术称为直接内存访问 (DMA)。 Windows 设备驱动程序开发人员提供了一个 DMA 库。

驱动程序 DMA 的详细信息，请参阅[DMA](https://msdn.microsoft.com/library/windows/hardware/ff544058)。

DMA 例程的列表，请参阅[直接内存访问 (DMA) 库例程](https://msdn.microsoft.com/library/windows/hardware/ff544068)。

请注意，DMA 是用于设备和内存之间直接进行通信的技术，并且不与相同[设备的内存访问](https://msdn.microsoft.com/library/windows/hardware/ff543138)，这是一组宏提供用于读取和写入到 I/O 端口和 CPU 寄存器。

 

 




