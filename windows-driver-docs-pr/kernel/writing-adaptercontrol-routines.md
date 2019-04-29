---
title: 编写 AdapterControl 例程
description: 编写 AdapterControl 例程
ms.assetid: a5a7501f-ba4f-441e-be07-6a1b7fac9938
keywords:
- AdapterControl 例程编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95981bdbe032b437ea7da6976dd003a9abacca30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384537"
---
# <a name="writing-adaptercontrol-routines"></a>编写 AdapterControl 例程





DMA 的设备的大多数驱动程序有[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程，它负责启动 DMA 操作。 (不需要的驱动程序*AdapterControl*例程包括的[使用散播-聚集 DMA](using-scatter-gather-dma.md)它们的[使用常见缓冲区、 总线 master DMA](using-common-buffer-bus-master-dma.md)。)

当驱动程序调用[ **AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573)，将其*AdapterControl*如果系统 DMA 控制器或主机总线适配器可用于立即运行例程DMA 操作，如果不够映射寄存器和都可用。 否则为*AdapterControl*例程会排队，直到这些资源都可用。

如果驱动程序的*AdapterControl*例程返回**KeepObject**或**DeallocateObjectKeepRegisters** (因此保留系统 DMA 控制器通道或主总线适配器的其他传输操作），驱动程序的[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程负责释放适配器对象或映射通过调用注册[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)或[ **FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513) DPC 之前例程完成当前的 IRP，并返回控件。

 

 




