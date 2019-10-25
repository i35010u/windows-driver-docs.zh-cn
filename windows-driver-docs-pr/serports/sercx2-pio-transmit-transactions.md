---
title: SerCx2 PIO-Transmit 事务
description: SerCx2 要求所有串行控制器驱动程序都实现对使用程控 i/o （PIO）的传输事务的支持。
ms.assetid: 3BEF9A3D-1FEF-4626-B07F-1670359062AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52451ab419507bd7759840fa99e3fc11ce2fcbe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845401"
---
# <a name="sercx2-pio-transmit-transactions"></a>SerCx2 PIO-Transmit 事务

SerCx2 要求所有串行控制器驱动程序都实现对使用程控 i/o （PIO）的传输事务的支持。 若要启动 PIO 传输事务，SerCx2 将调用驱动程序的[*EvtSerCx2PioTransmitWriteBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)事件回调函数并将写入缓冲区作为参数提供。

在此调用期间， *EvtSerCx2PioTransmitWriteBuffer*函数将数据从写入缓冲区传输到串行控制器硬件中的传输 FIFO。 此数据传输将继续，直到写入缓冲区为空或传输 FIFO 无法立即接受更多数据。 当传输结束时，函数将返回成功从写入缓冲区传输到 FIFO 的字节数。

## <a name="creating-the-pio-transmit-object"></a>创建 PIO 传输对象

在 SerCx2 可以调用任何串行控制器驱动程序的*EvtSerCx2PioTransmit*Xxx * * 函数之前，驱动程序必须调用[**SerCx2PioTransmitCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)方法将这些函数注册到 SerCx2。 此方法接受作为输入参数的指针，指向[**SERCX2\_PIO\_传输\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_pio_transmit_config)结构，该结构包含指向驱动程序的*EvtSerCx2PioTransmit*Xxx * * 函数的指针。

需要驱动程序才能实现以下三个函数：

- [*EvtSerCx2PioTransmitWriteBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)
- [*EvtSerCx2PioTransmitEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)
- [*EvtSerCx2PioTransmitCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)

作为选项，驱动程序可以实现以下一个或两个函数：

- [*EvtSerCx2PioTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)
- [*EvtSerCx2PioTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)

作为选项，驱动程序可以实现以下三个函数：

- [*EvtSerCx2PioTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)
- [*EvtSerCx2PioTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)
- [*EvtSerCx2PioTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_purge_fifo)

如果驱动程序实现前面列表中的任何函数，则它必须实现所有三个。

**SerCx2PioTransmitCreate**方法创建一个 PIO 传输对象，并向该对象的[**SERCX2PIOTRANSMIT**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)句柄提供调用驱动程序。 驱动程序的*EvtSerCx2PioTransmit*Xxx * * 函数全部使用此句柄作为其第一个参数。 以下 SerCx2 方法使用此句柄作为其第一个参数：

- [**SerCx2PioTransmitReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitready)
- [**SerCx2PioTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)
- [**SerCx2PioTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)
- [**SerCx2PioTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete)
- [**SerCx2PioTransmitPurgeFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitpurgefifocomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要在启动 PIO 传输事务时初始化串行控制器硬件，或在事务结束时清理串行控制器的硬件状态。

如果驱动程序实现了[*EvtSerCx2PioTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)事件回调函数，SerCx2 将调用此函数以在启动该事务的*EvtSerCx2PioTransmitWriteBuffer*调用之前初始化串行控制器。 如果实现，则*EvtSerCx2PioTransmitInitializeTransaction*函数必须调用[**SerCx2PioTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)方法，以便在驱动程序完成串行控制器初始化后通知 SerCx2。

如果驱动程序实现了[*EvtSerCx2PioTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)事件回调函数，SerCx2 将调用此函数，以清理事务中最后一个*EvtSerCx2PioTransmitWriteBuffer*调用之后的硬件状态。 如果实现，则*EvtSerCx2PioTransmitInitializeTransaction*函数必须调用[**SerCx2PioTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)方法，以便在驱动程序完成串行控制器清理后通知 SerCx2。

## <a name="draining-and-purging-the-transmit-fifo"></a>排出和清除传输 FIFO

如果驱动程序可以在传输 FIFO 清空时进行检测，则串行控制器驱动程序应实现[*EvtSerCx2PioTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)事件回调函数。 如果实现了，则 SerCx2 将在 PIO 传输事务中的最后一个字节的数据写入到传输 FIFO 后调用此函数。 在此调用期间， *EvtSerCx2PioTransmitDrainFifo*函数通常允许在传输 FIFO 清空时触发中断，然后返回而不等待。 当 FIFO 处于清空时，驱动程序将调用[**SerCx2PioTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete)方法以通知 SerCx2。 仅在收到此通知后，SerCx2 完成与 PIO 传输事务关联的挂起写入（[**IRP\_MJ\_写入**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))）请求。

如果串行控制器驱动程序未实现*EvtSerCx2PioTransmitDrainFifo*函数，则 SerCx2 必须先验证传输 FIFO 是否已清空，才能完成挂起的写入请求。 不能保证写入 FIFO 的数据将传输，而不会产生很大的延迟。 完成写请求后，在 FIFO 中保留的任何数据可能会丢失，然后才能传输。 在成功完成写入请求时，这种意外的数据丢失可能会为发送请求的外设驱动程序带来可靠性问题。

实现*EvtSerCx2PioTransmitDrainFifo*函数的驱动程序还必须实现[*EvtSerCx2PioTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)和[*EvtSerCx2PioTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)事件回调函数。

*EvtSerCx2PioTransmitCancelDrainFifo*函数使 SerCx2 可以在完成前取消正在进行的 FIFO 排出操作。 如果写入请求超时或已取消，SerCx2 可能会取消此操作。 如果*EvtSerCx2PioTransmitCancelDrainFifo*函数成功取消了 FIFO 排出操作，此函数将返回**TRUE**。 如果返回值**为 TRUE** ，则保证串行控制器驱动程序未调用，并且不会调用**SerCx2PioTransmitDrainFifoComplete**。 如果返回值为**FALSE** ，则表示*EvtSerCx2PioTransmitDrainFifo*函数已调用或将很快调用**SerCx2PioTransmitDrainFifoComplete**。

如果与 PIO 传输事务关联的写入请求在完成前被取消或超时，则 SerCx2 会调用*EvtSerCx2PioTransmitPurgeFifo*函数（如果已实现），以丢弃可能仍在传输 FIFO 的所有未发送数据。 SerCx2 使用它从此函数获取的信息，告诉外设驱动程序已通过写入请求将多少字节的数据成功传输到外围设备。

## <a name="ready-notifications"></a>就绪通知

当*EvtSerCx2PioTransmitWriteBuffer*调用结束，因为传输 FIFO 无法立即接受更多数据时，SerCx2 必须等待完成 PIO 接收事务，直到稍后才能接受更多数据。 在这种情况下，SerCx2 会调用[*EvtSerCx2PioTransmitEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)事件回调函数，使串行控制器驱动程序可以发送就绪通知。 如果启用了此通知，则串行控制器驱动程序将调用[**SerCx2PioTransmitReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitready)方法，以便在驱动程序检测到传输 FIFO 已准备好接受更多数据时通知 SerCx2。 为响应此通知，SerCx2 调用*EvtSerCx2PioTransmitWriteBuffer*函数将更多数据写入 FIFO。

如果在写入请求超时时启用了就绪通知，则 SerCx2 将调用[*EvtSerCx2PioTransmitCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)事件回调函数以取消挂起的通知。 如果此函数成功取消了挂起的通知，则返回**TRUE**。 如果返回值**为 TRUE** ，则保证串行控制器驱动程序将不会调用**SerCx2PioTransmitReady**。 如果返回值为**FALSE** ，则表示*EvtSerCx2PioTransmitDrainFifo*函数已调用或将调用**SerCx2PioTransmitReady**。
