---
title: SerCx2 Custom-Receive 事务
description: 某些串行控制器硬件可能会实现 PIO 或系统 DMA 以外的数据传输机制，以便从串行控制器读取数据。
ms.assetid: 29849A8C-6656-444C-BE91-405A4BA2D5B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b51b68706dd71ae8db8c5a11b799d5c2ce33a890
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349663"
---
# <a name="sercx2-custom-receive-transactions"></a>SerCx2 Custom-Receive 事务

某些串行控制器硬件可能会实现 PIO 或系统 DMA 以外的数据传输机制，以便从串行控制器读取数据。 串行控制器驱动程序可以支持自定义接收事务，以使 SerCx2 可以使用此数据传输机制。

若要启动自定义接收事务，SerCx2 将调用驱动程序的 [*EvtSerCx2CustomReceiveTransactionStart*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start) 事件回调函数，并将其作为参数提供给读取 ( [**IRP \_ MJ \_ read**](/previous-versions/ff546883(v=vs.85))) 请求和事务读取缓冲区的说明。 在此调用中，函数启动事务并返回。 然后，该驱动程序负责完成该事务并完成读取请求。

## <a name="creating-the-custom-receive-object"></a>创建自定义接收对象

在 SerCx2 可以调用任何串行控制器驱动程序的 *EvtSerCx2CustomReceiveTransaction* Xxx * * 函数之前，驱动程序必须调用 [**SerCx2CustomReceiveTransactionCreate**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate) 方法将这些函数注册到 SerCx2。 此方法接受作为输入参数的指针，该指针指向包含指向驱动程序的 *EvtSerCx2CustomReceiveTransaction* Xxx * * 函数的指针的 [**SERCX2 \_ 自定义 \_ 接收 \_ 事务 \_ 配置**](/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_custom_receive_transaction_config)结构。

驱动程序必须实现以下两个函数：

- [*EvtSerCx2CustomReceiveTransactionStart*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start)
- [*EvtSerCx2CustomReceiveTransactionQueryProgress*](/previous-versions/windows/hardware/drivers/dn265203(v=vs.85))

作为选项，驱动程序可以实现以下三个函数中的任何一个或全部：

- [*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*](/previous-versions/windows/hardware/drivers/dn265201(v=vs.85))
- [*EvtSerCx2CustomReceiveTransactionInitialize*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_initialize)
- [*EvtSerCx2CustomReceiveTransactionCleanup*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_cleanup)

**SerCx2CustomReceiveTransactionCreate** 方法创建自定义接收对象，并向调用驱动程序提供此对象的 [**SERCX2CUSTOMRECEIVETRANSACTION**](./sercx2-object-handles.md#sercx2customreceivetransaction-object-handle)句柄。 驱动程序的 *EvtSerCx2CustomReceiveTransaction* Xxx * * 函数全部使用此句柄作为其第一个参数。 以下 SerCx2 方法使用此句柄作为其第一个参数：

- [**SerCx2CustomReceiveTransactionNewDataNotification**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactionnewdatanotification)
- [**SerCx2CustomReceiveTransactionReportProgress**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactionreportprogress)
- [**SerCx2CustomReceiveTransactionInitializeComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioninitializecomplete)
- [**SerCx2CustomReceiveTransactionCleanupComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncleanupcomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要在自定义接收事务开始时初始化串行控制器硬件，或在事务结束时清理串行控制器的硬件状态。

如果驱动程序实现了 [*EvtSerCx2CustomReceiveTransactionInitialize*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_initialize) 事件回调函数，SerCx2 将在启动该事务之前调用此函数以初始化串行控制器。 如果实现，则 *EvtSerCx2CustomReceiveTransactionInitialize* 函数必须调用 [**SerCx2CustomReceiveTransactionInitializeComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioninitializecomplete) 方法，以便在驱动程序完成串行控制器初始化后通知 SerCx2。

如果驱动程序实现了 [*EvtSerCx2CustomReceiveTransactionCleanup*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_cleanup) 事件回调函数，SerCx2 将调用此函数以在事务结束后清理硬件状态。 如果实现，则 *EvtSerCx2CustomReceiveTransactionInitialize* 函数必须调用 [**SerCx2CustomReceiveTransactionCleanupComplete**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncleanupcomplete) 方法，以便在驱动程序完成串行控制器清理后通知 SerCx2。

## <a name="new-data-notifications"></a>新数据通知

作为选项，串行控制器驱动程序可以实现 [*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*](/previous-versions/windows/hardware/drivers/dn265201(v=vs.85)) 事件回调函数。 如果实现了此功能，SerCx2 将使用此函数来有效地管理处理作为自定义接收事务处理的读取请求期间发生的间隔超时。

如果串行控制器收到两个连续字节之间的间隔超出客户端指定的最长时间，则会出现间隔超时。 外围设备驱动程序将读取请求发送到 SerCx2 后，在从串行连接的外围设备收到至少一个字节的数据之前，将无法进行间隔超时。 在收到第一个字节之后，读取请求到达的时间与数据的第一个字节接收之间的时间可能比接收到读取请求的其余数据所需的时间长。 有关详细信息，请参阅 [**串行 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)。

如果实现了 SerCx2，则调用 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification* 函数以启用新的数据通知。 如果启用此通知，并且串行控制器接收来自外围设备的一个或多个字节的新数据，或者已在其接收 FIFO 中包含数据，则串行控制器驱动程序必须调用 [**SerCx2CustomReceiveTransactionNewDataNotification**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactionnewdatanotification) 方法以通知 SerCx2。

若要检测可能的间隔超时，SerCx2 会定期调用 [*EvtSerCx2CustomReceiveTransactionQueryProgress*](/previous-versions/windows/hardware/drivers/dn265203(v=vs.85)) 事件回调函数，以检查前面时间间隔内是否接收到任何数据。 SerCx2 如何检测数据的第一个字节的接收取决于串行控制器驱动程序是否实现了 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification* 函数。 如果实现了此函数，SerCx2 将调用函数以启用新的数据通知，并在收到第一个字节的数据时由驱动程序通知。 否则，SerCx2 会定期调用 *EvtSerCx2CustomReceiveTransactionQueryProgress* 函数来检测第一个字节的接收，并可能需要定期唤醒处理器才能进行这些调用。 因此，实现 *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification* 函数的驱动程序可以通过不要求处理器频繁唤醒来减少能耗。

SerCx2 不会为自定义接收事务显式取消挂起的新数据通知。 但是，如果启用了通知并且驱动程序必须根据以下原因之一完成关联的读取请求，则串行控制器驱动程序可能需要隐式取消新数据通知：

- 读取请求超时或已取消。
- 串行控制器即将退出 D0 设备电源状态以进入低功耗状态。

驱动程序通常会调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 等方法来完成请求。 请求完成后，驱动程序不得调用 **SerCx2CustomReceiveTransactionNewDataNotification** 。

## <a name="accessing-the-request-object"></a>访问请求对象

若要启动自定义接收事务，SerCx2 将调用驱动程序的 [*EvtSerCx2CustomReceiveTransactionStart*](/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start) 函数，并将关联的读取 (请求) 封装在 WDFREQUEST 对象句柄中，并将此函数作为参数传递给此函数。 在事务完成时，驱动程序负责调用方法（如 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) ）来完成该请求。 除非可以立即完成请求，否则，驱动程序必须调用方法（如 [**WdfRequestMarkCancelableEx**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) ）以将请求标记为可取消 *EvtSerCx2CustomReceiveTransactionStart* 。

串行控制器驱动程序不得使用 [**WdfRequestRetrieveOutputBuffer**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer) 等方法来访问读取请求中的数据缓冲区。 相反，驱动程序应使用传递给 *EvtSerCx2CustomReceiveTransactionStart* 函数的 *Mdl* 、 *Offset* 和 *Length* 参数值来访问此缓冲区。

在自定义接收事务期间，驱动程序可能需要在附加到请求对象的上下文中存储有关事务的信息。 如果是这样，驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 事件回调函数可以调用 [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes) 方法来设置用于请求对象的特性。 这些属性包括用于请求上下文的名称和分配大小。 在此调用中指定的请求属性必须与驱动程序在对 [**SerCx2InitializeDevice**](/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2initializedevice) 方法的调用中指定的请求属性匹配。 这些属性是在驱动程序传递给 **SerCx2InitializeDevice** 的 **SERCX2 \_ CONFIG** 结构的 **RequestAttributes** 成员中指定的。 有关详细信息，请参阅 [**SERCX2 \_ CONFIG**](/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_config)。

对于串行控制器驱动程序在自定义接收事务开始时接收的读取请求，驱动程序框架所分配的请求上下文未初始化。 作为最佳方案，驱动程序应调用 [**RtlZeroMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory) 例程将此请求上下文初始化为全部为零。