---
title: 启用 DMA 事务
description: 启用 DMA 事务
ms.assetid: 87735776-c371-425b-bc53-0c68375c9562
keywords:
- DMA 事务 WDK KMDF，启用
- DMA 操作 WDK KMDF，事务
- 主总线 DMA WDK KMDF 事务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e75b39f9d1ecb46c5b19bd6f370512ecf0aad033
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342829"
---
# <a name="enabling-dma-transactions"></a>启用 DMA 事务


\[仅适用于 KMDF\]




如果您基于 framework 的驱动程序处理 DMA 的设备的 I/O 操作，您的驱动程序必须启用 DMA 的每个设备的框架的 DMA 功能。 若要启用这些功能，您的驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)或[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数必须：

1.  调用[ **WdfDeviceSetAlignmentRequirement** ](https://msdn.microsoft.com/library/windows/hardware/ff546861)指定缓冲区对齐方式的设备的要求。

2.  调用[ **WdfDmaEnablerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546983)指定 DMA 操作 （单个数据包或分散/聚拢） 和设备支持的最大传输大小的类型。 从 KMDF 1.11 版开始，该框架支持[系统模式 DMA](supporting-system-mode-dma.md)芯片 (SoC) 上的系统上 – 基于 Windows 8 或更高版本的操作系统上运行的系统。

3.  调用[ **WdfDmaEnablerSetMaximumScatterGatherElements** ](https://msdn.microsoft.com/library/windows/hardware/ff547014)指定的最大设备可以支持散播-聚集列表中的元素数，如果设备支持散播-聚集操作。

下面的代码示例摘自[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)示例说明了如何启用框架的 DMA 功能。 此代码中出现*Init.c 文件*。

```cpp
WDF_DMA_ENABLER_CONFIG   dmaConfig;

WdfDeviceSetAlignmentRequirement( DevExt->Device, PCI9656_DTE_ALIGNMENT_16 );
WDF_DMA_ENABLER_CONFIG_INIT( &dmaConfig,
                             WdfDmaProfileScatterGather64Duplex,
                             DevExt->MaximumTransferLength );
status = WdfDmaEnablerCreate( DevExt->Device,
                              &dmaConfig, 
                              WDF_NO_OBJECT_ATTRIBUTES,
                              &DevExt->DmaEnabler );
```

如果您的驱动程序需要使用常见缓冲区，该驱动程序的*EvtDriverDeviceAdd*回调函数通常将这些设置。 有关这些缓冲区的详细信息，请参阅[使用常见缓冲区](using-common-buffers.md)。

驱动程序已调用后**WdfDmaEnablerCreate**，它可以调用[ **WdfDmaEnablerWdmGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff547020)以获取指向 WDM [ **DMA\_适配器**](https://msdn.microsoft.com/library/windows/hardware/ff544062)框架创建的设备的输入和输出方向的结构。 但是，大多数基于框架的驱动程序不需要访问这些结构。









