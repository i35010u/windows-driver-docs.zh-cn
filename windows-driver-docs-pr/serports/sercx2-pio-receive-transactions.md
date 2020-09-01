---
title: SerCx2 PIO-Receive 事务
description: SerCx2 要求所有串行控制器驱动程序都实现对使用程控 i/o (PIO) 的接收事务的支持。
ms.assetid: 00C43A55-ACAF-4AB6-BDFB-F3D9350C4536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 728d98486b04daaaa11d3d8b8b23af2373f76245
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186915"
---
# <a name="sercx2-pio-receive-transactions"></a>SerCx2 PIO-Receive 事务

SerCx2 要求所有串行控制器驱动程序都实现对使用程控 i/o (PIO) 的接收事务的支持。 若要启动 PIO 接收事务，SerCx2 将调用驱动程序的 [*EvtSerCx2PioReceiveReadBuffer*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer) 事件回调函数并将读取缓冲区作为参数提供。

在此调用期间， *EvtSerCx2PioReceiveReadBuffer* 函数将数据从串行控制器硬件中的 receive FIFO 传输到读取缓冲区。 此数据传输将继续，直到读取缓冲区已满，或者无法从 receive FIFO 立即获得更多数据。 当传输结束时，函数将返回成功从 FIFO 传输到读取缓冲区的字节数。 此函数永远不会等待接收更多数据。

## <a name="creating-the-pio-receive-object"></a>创建 PIO 接收对象

在 SerCx2 可以调用任何串行控制器驱动程序的 *EvtSerCx2PioReceive*Xxx * * 函数之前，驱动程序必须调用 [**SerCx2PioReceiveCreate**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate) 方法将这些函数注册到 SerCx2。 此方法接受作为输入参数的指针，该指针指向 [**SERCX2 \_ PIO \_ 接收 \_ 配置**](/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_pio_receive_config) 结构，该结构包含指向驱动程序的 *EvtSerCx2PioReceive*Xxx * * 函数的指针。

需要驱动程序才能实现以下三个函数：

- [*EvtSerCx2PioReceiveReadBuffer*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)
- [*EvtSerCx2PioReceiveEnableReadyNotification*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification)
- [*EvtSerCx2PioReceiveCancelReadyNotification*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification)

作为选项，驱动程序可以实现以下一个或两个函数：

- [*EvtSerCx2PioReceiveInitializeTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction)
- [*EvtSerCx2PioReceiveCleanupTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction)

**SerCx2PioReceiveCreate**方法创建一个 PIO 接收对象，并向该对象的[**SERCX2PIORECEIVE**](./sercx2-object-handles.md)句柄提供调用驱动程序。 驱动程序的 *EvtSerCx2PioReceive*Xxx * * 函数全部使用此句柄作为其第一个参数。 以下 SerCx2 方法使用此句柄作为其第一个参数：

- [**SerCx2PioReceiveReady**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveready)
- [**SerCx2PioReceiveInitializeTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete)
- [**SerCx2PioReceiveCleanupTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要在启动 PIO 接收事务时初始化串行控制器硬件，或在事务结束时清理串行控制器的硬件状态。

如果驱动程序实现了 [*EvtSerCx2PioReceiveInitializeTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction) 事件回调函数，SerCx2 将调用此函数以在启动该事务的 *EvtSerCx2PioReceiveReadBuffer* 调用之前初始化串行控制器。 如果实现，则 *EvtSerCx2PioReceiveInitializeTransaction* 函数必须调用 [**SerCx2PioReceiveInitializeTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete) 方法，以便在驱动程序完成串行控制器初始化后通知 SerCx2。

如果驱动程序实现了 [*EvtSerCx2PioReceiveCleanupTransaction*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction) 事件回调函数，SerCx2 将调用此函数，以清理事务中最后一个 *EvtSerCx2PioReceiveReadBuffer* 调用之后的硬件状态。 如果实现，则 *EvtSerCx2PioReceiveInitializeTransaction* 函数必须调用 [**SerCx2PioReceiveCleanupTransactionComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete) 方法，以便在驱动程序完成串行控制器清理后通知 SerCx2。

## <a name="ready-notifications"></a>就绪通知

当 *EvtSerCx2PioReceiveReadBuffer* 调用结束时，如果不能立即从 receive FIFO 中读取数据，SerCx2 将无法完成 PIO 接收事务，直到稍后，串行控制器才能接收更多数据。 在这种情况下，SerCx2 将调用 [*EvtSerCx2PioReceiveEnableReadyNotification*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification) 事件回调函数以启用就绪通知。 此函数通常允许在一个或多个字节的数据可从 receive FIFO 读取时触发中断。 当且仅当启用此通知时，串行控制器驱动程序会调用 [**SerCx2PioReceiveReady**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveready) 方法，以便在驱动程序检测到 receive FIFO 不再为空时通知 SerCx2。 为了响应此通知，SerCx2 调用 *EvtSerCx2PioReceiveReadBuffer* 函数来读取新接收的数据。

此外，SerCx2 还使用准备好的通知在处理作为 PIO 接收事务处理的读取请求期间有效地管理超时。 有关这些超时的详细信息，请参阅 [**串行 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)。

如果在读取请求超时时启用了就绪通知，则 SerCx2 将调用 [*EvtSerCx2PioReceiveCancelReadyNotification*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification) 事件回调函数以取消挂起的通知。 如果此函数成功取消了挂起的通知，则返回 **TRUE**。 如果返回值 **为 TRUE** ，则保证串行控制器驱动程序将不会调用 [**SerCx2PioReceiveReady**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveready)。 如果返回值为 **FALSE** ，则指示控制器驱动程序已调用或即将调用 **SerCx2PioReceiveReady**。