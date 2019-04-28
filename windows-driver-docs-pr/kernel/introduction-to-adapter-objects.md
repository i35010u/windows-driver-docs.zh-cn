---
title: 适配器对象简介
description: 适配器对象简介
ms.assetid: a1a0d516-dee0-484a-b971-c7a595fef155
keywords:
- AdapterControl 例程，有关 AdapterControl 例程
- DMA 传输 WDK 内核，适配器对象
- 适配器对象 WDK 内核，有关适配器的对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31ac4e12cb2be8461be0d06dd61d653f83737664
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341067"
---
# <a name="introduction-to-adapter-objects"></a>适配器对象简介





使用直接 I/O 和 DMA 任何驱动程序必须创建的适配器对象。 该适配器对象表示 DMA 控制器通道或端口或总线母版设备。

两种类型的最低级别的驱动程序必须使用适配器对象：

-   使用系统 DMA 控制器的设备的驱动程序。 此类设备称为*从属设备*说到"使用系统 (或*从属*) DMA。"

-   用于将主机总线适配器的设备驱动程序。 此类设备与 I/O 总线中，使用系统进行仲裁，并因此使用总线 master DMA。

驱动程序提供存储，通常在设备扩展中，对指向适配器对象的指针。

若要执行 DMA 传输，通常使用任一 DMA 方法的设备的驱动程序具有[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程和调用系统提供支持例程，操作适配器对象。 (不需要的驱动程序*AdapterControl*例程包括的[使用散播-聚集 DMA](using-scatter-gather-dma.md)它们的[使用常见缓冲区、 总线 master DMA](using-common-buffer-bus-master-dma.md)。)

设备启动操作，句柄 DMA 操作调用 I/O 管理器中，驱动程序的一部分，在打开创建的适配器对象的一组调用特定于平台的 HAL。 任何 Windows 平台上的适配器对象的集合通常包括一个适配器对象，用于：

-   每个系统 DMA 控制器通道或从属设备附加到的端口。

-   在计算机中每个主总线 DMA 设备。

（对于 SCSI 设备支持的总线 master DMA，SCSI 端口驱动程序设置了特定于 HBA 的 SCSI 微型端口驱动程序的适配器对象。 微型端口驱动程序[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)例程提供端口驱动程序使用特定于适配器的数据。)

请参阅[使用系统 DMA](using-system-dma.md)并[使用总线 Master DMA](using-bus-master-dma.md)有关驱动程序何时以及如何使用适配器对象的详细信息并*AdapterControl*例程。

 

 




