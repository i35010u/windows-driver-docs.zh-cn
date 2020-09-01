---
title: SerCx2 System-DMA-Transmit 事务
description: 某些串行控制器驱动程序实现对使用系统 DMA 控制器的传输事务的支持。
ms.assetid: 8569E76F-CAFF-4A2C-8052-62B340C5ADED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dc698708969a2b418a202eb738e20e944d02042
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189053"
---
# <a name="sercx2-system-dma-transmit-transactions"></a>SerCx2 System-DMA-Transmit 事务

某些串行控制器驱动程序实现对使用系统 DMA 控制器的传输事务的支持。 此类支持是可选的，但可以通过在长时间数据传输中免除使用程控 i/o (PIO) ，从而提高性能。 SerCx2 通过设置系统 DMA 控制器并代表串行控制器驱动程序启动必需的 DMA 传输，来执行系统 DMA 传输事务。

当串行控制器驱动程序创建系统 DMA 传输对象时，驱动程序将提供参数，SerCx2 将使用这些参数为系统 DMA 传输事务设置系统 DMA 适配器。

在开始事务之前，串行控制器驱动程序可以选择对该事务可能需要的串行控制器硬件或 DMA 适配器进行任何特殊设置。 事务完成后，驱动程序可以选择排出传输 FIFO，并在必要时清除串行控制器硬件状态。

## <a name="creating-the-system-dma-transmit-object"></a>创建系统 DMA 传输对象

在 SerCx2 可以调用任何串行控制器驱动程序的 *EvtSerCx2SystemDmaTransmit*Xxx * * 函数之前，驱动程序必须调用 [**SerCx2SystemDmaTransmitCreate**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate) 方法将这些函数注册到 SerCx2。 此方法接受作为输入参数的指针，该指针指向 [**SERCX2 \_ 系统 \_ DMA \_ 传输 \_ 配置**](/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_system_dma_transmit_config) 结构，该结构包含指向驱动程序的 *EvtSerCx2SystemDmaTransmit*Xxx * * 函数的指针。

作为选项，驱动程序可以实现以下任何或全部函数：

- [*EvtSerCx2SystemDmaTransmitInitializeTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_initialize_transaction)
- [*EvtSerCx2SystemDmaTransmitCleanupTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cleanup_transaction)
- [*EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_configure_dma_channel)

作为选项，驱动程序可以实现以下功能：

- [*EvtSerCx2SystemDmaTransmitDrainFifo*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_drain_fifo)
- [*EvtSerCx2SystemDmaTransmitCancelDrainFifo*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cancel_drain_fifo)
- [*EvtSerCx2SystemDmaTransmitPurgeFifo*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_purge_fifo)

实现上述列表中的任何函数的驱动程序必须实现全部三个。

**SerCx2SystemDmaTransmitCreate**方法创建一个系统 DMA 传输对象，并向调用驱动程序提供此对象的[**SERCX2SYSTEMDMATRANSMIT**](./sercx2-object-handles.md#sercx2systemdmatransmit-object-handle)句柄。 驱动程序的 *EvtSerCx2SystemDmaTransmit*Xxx * * 函数全部使用此句柄作为其第一个参数。 以下 SerCx2 方法使用此句柄作为其第一个参数：

- [**SerCx2SystemDmaTransmitDrainFifoComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitdrainfifocomplete)
- [**SerCx2SystemDmaTransmitPurgeFifoComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitpurgefifocomplete)
- [**SerCx2SystemDmaTransmitInitializeTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitinitializetransactioncomplete)
- [**SerCx2SystemDmaTransmitCleanupTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcleanuptransactioncomplete)
- [**SerCx2SystemDmaTransmitGetDmaEnabler**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitgetdmaenabler)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要在系统 DMA 传输事务开始时初始化串行控制器硬件，或在事务结束时清理串行控制器的硬件状态。

如果驱动程序实现了 [*EvtSerCx2SystemDmaTransmitInitializeTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_initialize_transaction) 事件回调函数，则在事务中开始第一个 DMA 传输之前，SerCx2 将调用此函数以初始化串行控制器。 如果实现，则 *EvtSerCx2SystemDmaTransmitInitializeTransaction* 函数必须调用 [**SerCx2SystemDmaTransmitInitializeTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitinitializetransactioncomplete) 方法，以便在驱动程序完成串行控制器初始化后通知 SerCx2。

如果驱动程序实现了 [*EvtSerCx2SystemDmaTransmitCleanupTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cleanup_transaction) 事件回调函数，SerCx2 将调用此函数，以清除事务中最后一个 DMA 传输结束后的硬件状态。 如果实现，则 *EvtSerCx2SystemDmaTransmitInitializeTransaction* 函数必须调用 [**SerCx2SystemDmaTransmitCleanupTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcleanuptransactioncomplete) 方法，以便在驱动程序完成串行控制器清理后通知 SerCx2。

在系统 DMA 传输事务开始时，需要对系统 DMA 控制器进行任何特殊配置的串行控制器驱动程序应实现 [*EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_configure_dma_channel) 事件回调函数。 此函数可以调用 [**SerCx2SystemDmaTransmitGetDmaEnabler**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitgetdmaenabler) 方法以获取用于事务的系统 dma 适配器的 DMA 启用程序。 SerCx2 在启动事务中的第一个 DMA 传输之前调用此函数。 有关 DMA 启用码的详细信息，请参阅 [启用 Dma 事务](../wdf/enabling-dma-transactions.md)。

## <a name="draining-and-purging-the-transmit-fifo"></a>排出和清除传输 FIFO

支持系统 DMA 传输事务的串行控制器驱动程序应实现 [*EvtSerCx2SystemDmaTransmitDrainFifo*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_drain_fifo) 事件回调函数（如果驱动程序可以在传输 FIFO 清空时进行检测）。 如果实现，SerCx2 将在系统 DMA 传输事务中的最后一个字节的数据写入到传输 FIFO 后调用此函数。 在此调用过程中， *EvtSerCx2SystemDmaTransmitDrainFifo* 函数通常会启用当传输 FIFO 清空时触发的中断，然后返回而不等待中断。 当 FIFO 处于清空时，驱动程序将调用 [**SerCx2SystemDmaTransmitDrainFifoComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitdrainfifocomplete) 方法以通知 SerCx2。 仅在收到此通知后，SerCx2 完成与系统 DMA 传输事务相关联的写入 ([**IRP \_ MJ \_ 写入**](/previous-versions/ff546904(v=vs.85))) 请求。

如果串行控制器驱动程序未实现 *EvtSerCx2SystemDmaTransmitDrainFifo* 函数，则 SerCx2 必须先验证传输 FIFO 是否已清空，才能完成挂起的写入请求。 不能保证写入 FIFO 的数据将传输，而不会产生很大的延迟。 完成写请求后，在 FIFO 中保留的任何数据可能会丢失，然后才能传输。 在成功完成写入请求时，这种意外的数据丢失可能会为发送请求的外设驱动程序带来可靠性问题。

实现 *EvtSerCx2SystemDmaTransmitDrainFifo* 函数的驱动程序还必须实现 [*EvtSerCx2SystemDmaTransmitCancelDrainFifo*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cancel_drain_fifo) 和 [*EvtSerCx2SystemDmaTransmitPurgeFifo*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_purge_fifo) 事件回调函数。

*EvtSerCx2SystemDmaTransmitCancelDrainFifo*函数使 SerCx2 可以在完成前取消正在进行的 FIFO 排出操作。 如果写入请求已取消，或者串行控制器即将退出 D0 设备电源状态以进入低功耗状态，SerCx2 可能会取消此操作。 如果 *EvtSerCx2SystemDmaTransmitCancelDrainFifo* 函数成功取消了 FIFO 排出操作，此函数将返回 **TRUE**。 如果返回值 **为 TRUE** ，则确保 *EvtSerCx2SystemDmaTransmitDrainFifo* 函数在不首先调用 **SerCx2SystemDmaTransmitDrainFifoComplete**的情况下返回。 如果返回值为 **FALSE** ，则表示 *EvtSerCx2SystemDmaTransmitDrainFifo* 函数已调用或将调用 **SerCx2SystemDmaTransmitDrainFifoComplete**。

如果与系统 DMA 传输事务关联的写入请求在完成前被取消或超时，则 SerCx2 会调用 *EvtSerCx2SystemDmaTransmitPurgeFifo* 函数（如果已实现），以丢弃可能仍在传输 FIFO 的所有未发送数据。 清除 FIFO 后， *EvtSerCx2SystemDmaTransmitPurgeFifo* 函数将调用 [**SerCx2SystemDmaTransmitPurgeFifoComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitpurgefifocomplete) 方法来通知 SerCx2。 仅在收到此通知后，SerCx2 开始新的 i/o 事务。