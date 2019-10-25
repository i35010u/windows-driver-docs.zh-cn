---
title: SerCx2 System-DMA-Receive 事务
description: 某些串行控制器驱动程序实现对使用系统 DMA 控制器的接收事务的支持。
ms.assetid: 0374D1BE-96ED-43D6-8661-5E9676B82C0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d0640b8f1ab9a3af7d612d054a0a93ea26eeca4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845400"
---
# <a name="sercx2-system-dma-receive-transactions"></a>SerCx2 System-DMA-Receive 事务

某些串行控制器驱动程序实现对使用系统 DMA 控制器的接收事务的支持。 此类支持是可选的，但可以通过免除用于长时间数据传输的程控 i/o （PIO）的主要处理器来提高性能。 SerCx2 通过设置系统 DMA 控制器并代表串行控制器驱动程序启动必需的 DMA 传输，来执行系统 DMA 接收事务。

当串行控制器驱动程序创建系统 DMA 接收对象时，驱动程序将提供参数，SerCx2 将使用这些参数为系统 DMA 接收事务设置系统 DMA 适配器。

在开始使用系统 DMA 接收事务之前，串行控制器驱动程序可以选择对事务可能需要的串行控制器硬件或 DMA 适配器进行任何特殊设置。 事务完成后，驱动程序可以（如有必要）对任何可能需要的串行控制器硬件状态进行清理。

## <a name="creating-the-system-dma-receive-object"></a>创建系统 DMA 接收对象

在 SerCx2 可以调用任何串行控制器驱动程序的*EvtSerCx2SystemDmaReceive*Xxx * * 函数之前，驱动程序必须调用[**SerCx2SystemDmaReceiveCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)方法将这些函数注册到 SerCx2。 此方法接受作为输入参数的指针，该指针指向[**SERCX2\_SYSTEM\_DMA\_接收\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_system_dma_receive_config)结构，该结构包含指向驱动程序的*EvtSerCx2SystemDmaReceive*Xxx * * 函数的指针。

作为选项，驱动程序可以实现以下任何或全部函数：

- [*EvtSerCx2SystemDmaReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_initialize_transaction)
- [*EvtSerCx2SystemDmaReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cleanup_transaction)
- [*EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_configure_dma_channel)

作为选项，驱动程序可以实现以下两个函数：

- [*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_enable_new_data_notification)
- [*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cancel_new_data_notification)

实现上述列表中的两个函数之一的驱动程序必须实现两者。

**SerCx2SystemDmaReceiveCreate**方法创建一个系统 DMA 接收对象，并向调用驱动程序提供此对象的[**SERCX2SYSTEMDMARECEIVE**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)句柄。 驱动程序的*EvtSerCx2SystemDmaReceive*Xxx * * 函数全部使用此句柄作为其第一个参数。 以下 SerCx2 方法使用此句柄作为其第一个参数：

- [**SerCx2SystemDmaReceiveNewDataNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivenewdatanotification)
- [**SerCx2SystemDmaReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceiveinitializetransactioncomplete)
- [**SerCx2SystemDmaReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecleanuptransactioncomplete)
- [**SerCx2SystemDmaReceiveGetDmaEnabler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivegetdmaenabler)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要在系统 DMA 接收事务开始时初始化串行控制器硬件，或在事务结束时清理串行控制器的硬件状态。

如果驱动程序实现了[*EvtSerCx2SystemDmaReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_initialize_transaction)事件回调函数，则在事务中开始第一个 DMA 传输之前，SerCx2 将调用此函数以初始化串行控制器。 如果实现，则*EvtSerCx2SystemDmaReceiveInitializeTransaction*函数必须调用[**SerCx2SystemDmaReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceiveinitializetransactioncomplete)方法，以便在驱动程序完成串行控制器初始化后通知 SerCx2。

如果驱动程序实现了[*EvtSerCx2SystemDmaReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cleanup_transaction)事件回调函数，SerCx2 将调用此函数，以清除事务中最后一个 DMA 传输结束后的硬件状态。 如果实现，则*EvtSerCx2SystemDmaReceiveInitializeTransaction*函数必须调用[**SerCx2SystemDmaReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecleanuptransactioncomplete)方法，以便在驱动程序完成串行控制器清理后通知 SerCx2。

需要在系统 DMA 接收事务开始时对系统 DMA 控制器进行任何特殊配置的串行控制器驱动程序应实现[*EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_configure_dma_channel)事件回调函数。 此函数可以调用[**SerCx2SystemDmaReceiveGetDmaEnabler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivegetdmaenabler)方法以获取用于事务的系统 dma 适配器的 DMA 启用程序。 SerCx2 在启动事务中的第一个 DMA 传输之前调用此函数。 有关 DMA 启用码的详细信息，请参阅[启用 Dma 事务](https://docs.microsoft.com/windows-hardware/drivers/wdf/enabling-dma-transactions)。

## <a name="new-data-notifications"></a>新数据通知

作为选项，串行控制器驱动程序可以实现[*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_enable_new_data_notification)事件回调函数。 如果实现，SerCx2 将使用此函数在处理作为系统 DMA 接收事务处理的读取请求期间有效地管理间隔超时。

如果串行控制器收到两个连续字节之间的间隔超出客户端指定的最长时间，则会出现间隔超时。 外围设备驱动程序将读取请求发送到 SerCx2 后，在从串行连接的外围设备收到至少一个字节的数据之前，将无法进行间隔超时。 在收到第一个字节之后，读取请求到达的时间与数据的第一个字节接收之间的时间可能比接收到读取请求的其余数据所需的时间长。 有关详细信息，请参阅[**串行\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)。

如果实现了 SerCx2，则调用*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*函数以启用*新的数据通知*。 如果启用此通知，并且串行控制器接收来自外围设备的一个或多个字节的新数据，或者已在其接收 FIFO 中包含数据，则串行控制器驱动程序必须调用[**SerCx2SystemDmaReceiveNewDataNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivenewdatanotification)用于通知 SerCx2 的方法。

为了检测可能的间隔超时，SerCx2 会定期调用系统 DMA 适配器的[**ReadDmaCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter)例程来检查前面时间间隔内是否接收到任何数据。 SerCx2 如何检测数据的第一个字节的接收取决于串行控制器驱动程序是否实现了*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*函数。 如果实现了此函数，SerCx2 将调用函数以启用新的数据通知，并在收到第一个字节的数据时由驱动程序通知。 否则，SerCx2 会定期调用**ReadDmaCounter**来检测第一个字节的接收，并可能需要定期唤醒处理器来进行这些调用。 因此，实现*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*函数的驱动程序可以通过不要求处理器频繁唤醒来减少能耗。

**请注意**  SerCx2 依赖于系统 dma 适配器的**ReadDmaCounter**例程来监视系统 dma 接收事务和系统 dma 传输事务的超时时间。 硬件抽象层（HAL）必须为用于在串行控制器之间传输数据的系统 DMA 控制器实现一个功能完备的**ReadDmaCounter**例程。

支持针对系统 DMA 接收事务的新数据通知的串行控制器驱动程序必须实现[*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cancel_new_data_notification)事件回调函数，以便 SerCx2 可以取消已启用的新数据通知。 如果在取消挂起的读取请求时或发生总超时时启用了新的数据通知，则 SerCx2 将调用*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*函数以取消通知。 如果此函数成功取消了挂起的通知，则返回**TRUE**。 如果返回值**为 TRUE** ，则保证串行控制器驱动程序将不会调用**SerCx2SystemDmaReceiveNewDataNotification**。 如果返回值为**FALSE** ，则表示驱动程序已调用或将很快调用**SerCx2SystemDmaReceiveNewDataNotification**。 有关总超时的详细信息，请参阅[**串行\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)。
