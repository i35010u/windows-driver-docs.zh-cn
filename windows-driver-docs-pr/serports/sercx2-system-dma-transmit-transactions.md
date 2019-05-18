---
title: SerCx2 System-DMA-Transmit 事务
description: 某些串行控制器驱动程序实现对支持传输使用系统 DMA 控制器的事务。
ms.assetid: 8569E76F-CAFF-4A2C-8052-62B340C5ADED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6173739032750c41945190fc86e2f33745dea019
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836323"
---
# <a name="sercx2-system-dma-transmit-transactions"></a>SerCx2 System-DMA-Transmit 事务

某些串行控制器驱动程序实现对支持传输使用系统 DMA 控制器的事务。 这种支持是可选的但可以提高性能，因为它使主处理器需要的用于通过编程方式设置 I/O (PIO) 的长整型数据传输。 SerCx2 执行设置了系统 DMA 控制器并启动代表串行控制器驱动程序的必要 DMA 传输系统 DMA 传输的事务。

串行控制器驱动程序创建系统 DMA 传输对象时，驱动程序提供 SerCx2 将用于设置系统 DMA 传输的事务的系统 DMA 适配器的参数。

在事务开始时之前, 串行控制器驱动程序存在执行串行控制器硬件或 DMA 适配器可能需要事务的任何特殊设置的选项。 该驱动程序在事务完成后，可以选择以清空传输 FIFO，并且如有必要，以清理串行控制器硬件状态。

## <a name="creating-the-system-dma-transmit-object"></a>创建系统 DMA 传输对象

SerCx2 可以调用任何串行控制器驱动程序之前*EvtSerCx2SystemDmaTransmit*Xxx * * 函数，该驱动程序必须调用[ **SerCx2SystemDmaTransmitCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn265288)方法以向 SerCx2 注册这些函数。 此方法接受，作为输入参数，一个指向[ **SERCX2\_系统\_DMA\_传输\_配置**](https://msdn.microsoft.com/library/windows/hardware/dn265344)结构，其中包含驱动程序的指针*EvtSerCx2SystemDmaTransmit*Xxx * * 函数。

作为一个选项，该驱动程序可以实现任何或所有以下函数：

- [*EvtSerCx2SystemDmaTransmitInitializeTransaction*](https://msdn.microsoft.com/library/windows/hardware/dn265237)
- [*EvtSerCx2SystemDmaTransmitCleanupTransaction*](https://msdn.microsoft.com/library/windows/hardware/dn265234)
- [*EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](https://msdn.microsoft.com/library/windows/hardware/dn265235)

作为一个选项，该驱动程序可以实现以下功能：

- [*EvtSerCx2SystemDmaTransmitDrainFifo*](https://msdn.microsoft.com/library/windows/hardware/dn265236)
- [*EvtSerCx2SystemDmaTransmitCancelDrainFifo*](https://msdn.microsoft.com/library/windows/hardware/dn265233)
- [*EvtSerCx2SystemDmaTransmitPurgeFifo*](https://msdn.microsoft.com/library/windows/hardware/dn265238)

实现的任何函数前面的列表中的驱动程序必须实现所有这三个。

**SerCx2SystemDmaTransmitCreate**方法创建系统 DMA 传输对象，并提供与调用驱动程序[ **SERCX2SYSTEMDMATRANSMIT** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles#sercx2systemdmatransmit-object-handle)这句柄对象。 在驱动程序*EvtSerCx2SystemDmaTransmit*Xxx * * 函数所有采用该句柄作为其第一个参数。 以下 SerCx2 方法将此句柄作为其第一个参数：

- [**SerCx2SystemDmaTransmitDrainFifoComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265289)
- [**SerCx2SystemDmaTransmitPurgeFifoComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265307)
- [**SerCx2SystemDmaTransmitInitializeTransactionComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265306)
- [**SerCx2SystemDmaTransmitCleanupTransactionComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265286)
- [**SerCx2SystemDmaTransmitGetDmaEnabler**](https://msdn.microsoft.com/library/windows/hardware/dn265305)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

初始化一个系统 DMA 传输的事务，开始时的串行控制器硬件或清理该事务结束时的串行控制器的硬件状态，可能需要某些串行控制器驱动程序。

如果驱动程序实现[ *EvtSerCx2SystemDmaTransmitInitializeTransaction* ](https://msdn.microsoft.com/library/windows/hardware/dn265237)事件回调函数，SerCx2 调用此函数可在开始第一个 DMA 之前初始化串行控制器传输在事务中。 如果实现，则*EvtSerCx2SystemDmaTransmitInitializeTransaction*函数必须调用[ **SerCx2SystemDmaTransmitInitializeTransactionComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265306)要初始化的串行控制器驱动程序完成时通知 SerCx2 方法。

如果该驱动程序实现[ *EvtSerCx2SystemDmaTransmitCleanupTransaction* ](https://msdn.microsoft.com/library/windows/hardware/dn265234)事件回调函数，SerCx2 调用此函数以进行最终 DMA 传输结束后清除硬件状态在事务中。 如果实现，则*EvtSerCx2SystemDmaTransmitInitializeTransaction*函数必须调用[ **SerCx2SystemDmaTransmitCleanupTransactionComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265286)方法若要清理串行控制器驱动程序完成时通知 SerCx2。

需要执行任何特殊配置的传输系统 DMA 事务开始时的系统 DMA 控制器的串行控制器驱动程序应实现[ *EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](https://msdn.microsoft.com/library/windows/hardware/dn265235)事件回调函数。 此函数可以调用[ **SerCx2SystemDmaTransmitGetDmaEnabler** ](https://msdn.microsoft.com/library/windows/hardware/dn265305)方法以获取有关使用事务的系统 DMA 适配器 DMA 促成因素。 SerCx2 开始在事务中的第一个 DMA 传输之前调用此函数。 DMA 实现方法的详细信息，请参阅[启用 DMA 事务](https://msdn.microsoft.com/library/windows/hardware/ff540818)。

## <a name="draining-and-purging-the-transmit-fifo"></a>排出和清除传输先进先出

支持系统 DMA 传输的事务的串行控制器驱动程序应实现[ *EvtSerCx2SystemDmaTransmitDrainFifo* ](https://msdn.microsoft.com/library/windows/hardware/dn265236)如果驱动程序可以检测何时事件回调函数传输先进先出清空。 如果实现，SerCx2 后会立即调用此函数系统 DMA 传输事务中的数据的最后一个字节写入传输先进先出。 在此调用期间*EvtSerCx2SystemDmaTransmitDrainFifo*函数通常情况下允许传输 FIFO 清空时，会触发中断，然后返回而无需等待中断。 当先进先出清空时，驱动程序会调用[ **SerCx2SystemDmaTransmitDrainFifoComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265289)方法以通知 SerCx2。 仅在收到此通知后不会 SerCx2 完成正在等待的写入 ([**IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) 与系统-DMA 的传输相关联的请求事务。

如果串行控制器驱动程序不实现*EvtSerCx2SystemDmaTransmitDrainFifo*函数，SerCx2 必须完成正在等待的写入请求，而没有首先验证传输 FIFO 已清空。 可以将被写入到先进先出的数据传输而无需较长的延迟不能保证。 可以传输之前，在写请求完成后，仍保持先进先出的任何数据可能会丢失。 已成功完成的写入请求中此意外的数据丢失可以创建将请求发送的外围设备驱动程序的可靠性问题。

实现一个驱动程序*EvtSerCx2SystemDmaTransmitDrainFifo*函数还必须实现[ *EvtSerCx2SystemDmaTransmitCancelDrainFifo* ](https://msdn.microsoft.com/library/windows/hardware/dn265233)和[ *EvtSerCx2SystemDmaTransmitPurgeFifo* ](https://msdn.microsoft.com/library/windows/hardware/dn265238)事件回调函数。

*EvtSerCx2SystemDmaTransmitCancelDrainFifo*函数使 SerCx2 完成之前取消正在进行的先进先出排出操作。 如果写入请求已取消，或如果串行控制器即将退出 D0 设备电源状态进入低功耗状态，SerCx2 可能会取消此操作。 如果*EvtSerCx2SystemDmaTransmitCancelDrainFifo*函数已成功取消 FIFO 排出操作，此函数将返回**TRUE**。 返回值 **，则返回 TRUE**保证*EvtSerCx2SystemDmaTransmitDrainFifo*函数将返回而无需第一个调用**SerCx2SystemDmaTransmitDrainFifoComplete**. 返回值**FALSE**指示*EvtSerCx2SystemDmaTransmitDrainFifo*函数将调用，或已调用**SerCx2SystemDmaTransmitDrainFifoComplete**。

如果与传输系统 DMA 事务关联的写入请求被取消或时间出完成之前，SerCx2 调用*EvtSerCx2SystemDmaTransmitPurgeFifo*函数，如果它实现，放弃任何未发送可能会保持传输先进先出的数据。 时清除 FIFO *EvtSerCx2SystemDmaTransmitPurgeFifo*函数调用[ **SerCx2SystemDmaTransmitPurgeFifoComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265307)方法以通知 SerCx2。 仅在收到此通知后不 SerCx2 开始新的 I/O 事务。
