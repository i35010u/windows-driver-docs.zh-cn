---
title: SerCx2 Custom-Receive 事务
description: 某些串行控制器硬件可能会实现 PIO 或系统 DMA 以外的数据传输机制，用于从串行控制器中读取数据。
ms.assetid: 29849A8C-6656-444C-BE91-405A4BA2D5B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a95ac95e674c2a836916b87ebf1a7c370d7caab9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356812"
---
# <a name="sercx2-custom-receive-transactions"></a>SerCx2 Custom-Receive 事务

某些串行控制器硬件可能会实现 PIO 或系统 DMA 以外的数据传输机制，用于从串行控制器中读取数据。 串行控制器驱动程序支持自定义接收事务以 SerCx2 即可使用此数据传输机制。

若要开始自定义接收事务，SerCx2 调用驱动程序的[ *EvtSerCx2CustomReceiveTransactionStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start)事件回调函数并作为参数提供只读 ([ **IRP\_MJ\_读取**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))) 请求和读取缓冲区的事务的说明。 在此调用中，该函数启动事务，并返回。 然后，该驱动程序是负责完成该事务并完成读取的请求。

## <a name="creating-the-custom-receive-object"></a>创建 custom-receive 对象

SerCx2 可以调用任何串行控制器驱动程序之前*EvtSerCx2CustomReceiveTransaction*Xxx * * 函数，该驱动程序必须调用[ **SerCx2CustomReceiveTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioncreate)方法以向 SerCx2 注册这些函数。 此方法接受，作为输入参数，一个指向[ **SERCX2\_自定义\_接收\_事务\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_custom_receive_transaction_config)结构包含的驱动程序的指针*EvtSerCx2CustomReceiveTransaction*Xxx * * 函数。

该驱动程序必须实现以下两个函数：

- [*EvtSerCx2CustomReceiveTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start)
- [*EvtSerCx2CustomReceiveTransactionQueryProgress*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265203(v=vs.85))

作为一个选项，该驱动程序可以实现任何或所有以下三个函数：

- [*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265201(v=vs.85))
- [*EvtSerCx2CustomReceiveTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_initialize)
- [*EvtSerCx2CustomReceiveTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_cleanup)

**SerCx2CustomReceiveTransactionCreate**方法创建 custom-receive 对象，并提供与调用驱动程序[ **SERCX2CUSTOMRECEIVETRANSACTION** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handlessercx2customreceivetransaction-object-handle)此对象的句柄。 在驱动程序*EvtSerCx2CustomReceiveTransaction*Xxx * * 函数所有采用该句柄作为其第一个参数。 以下 SerCx2 方法将此句柄作为其第一个参数：

- [**SerCx2CustomReceiveTransactionNewDataNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactionnewdatanotification)
- [**SerCx2CustomReceiveTransactionReportProgress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactionreportprogress)
- [**SerCx2CustomReceiveTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioninitializecomplete)
- [**SerCx2CustomReceiveTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioncleanupcomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要初始化的开头的串行控制器硬件自定义接收事务，或清除该事务结束时的串行控制器的硬件状态。

如果驱动程序实现[ *EvtSerCx2CustomReceiveTransactionInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_initialize)事件回调函数，SerCx2 调用此函数可初始化之前启动的事务执行串行控制器。 如果实现，则*EvtSerCx2CustomReceiveTransactionInitialize*函数必须调用[ **SerCx2CustomReceiveTransactionInitializeComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioninitializecomplete)方法初始化串行控制器驱动程序完成时通知 SerCx2。

如果该驱动程序实现[ *EvtSerCx2CustomReceiveTransactionCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_cleanup)事件回调函数，SerCx2 调用此函数可在事务结束后清理硬件状态。 如果实现，则*EvtSerCx2CustomReceiveTransactionInitialize*函数必须调用[ **SerCx2CustomReceiveTransactionCleanupComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioncleanupcomplete)方法，从而通知SerCx2 清理串行控制器驱动程序完成。

## <a name="new-data-notifications"></a>新数据通知

作为一个选项，可以实现串行控制器驱动程序[ *EvtSerCx2CustomReceiveTransactionEnableNewDataNotification* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265201(v=vs.85))事件回调函数。 如果实现，SerCx2 使用此函数有效地管理的处理与自定义接收事务的读取请求的处理过程中发生的时间间隔超时值。

如果串行控制器收到的两个连续字节之间的间隔超出了客户端指定的最长时间，会发生间隔超时。 外围设备驱动程序将读取的请求发送到 SerCx2 后，间隔超时不能发生之前，至少一个字节的数据是从串行连接的外围设备收到。 之间的到达时间的读取的请求和外围设备中的数据的第一个字节的接收可能比所需接收的数据的读取请求的其余部分后接收到的第一个字节的时间。 有关详细信息，请参阅[**串行\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_timeouts)。

SerCx2 调用*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*函数，如果实现它后，若要启用的新数据通知。 如果启用了此通知并且串行控制器接收的新数据的一个或多个字节从外围设备，或已存在数据其接收 FIFO，串行控制器驱动程序必须调用[ **SerCx2CustomReceiveTransactionNewDataNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactionnewdatanotification)方法以通知 SerCx2。

若要检测可能间隔超时，SerCx2 定期调用[ *EvtSerCx2CustomReceiveTransactionQueryProgress* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn265203(v=vs.85))事件回调函数来检查是否在收到任何数据前一个时间间隔。 SerCx2 如何检测数据的第一个字节的回执取决于是否实现串行控制器驱动程序*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*函数。 如果执行此函数，SerCx2 调用函数来启用新数据通知和接收数据的第一个字节时驱动程序收到通知。 否则，SerCx2 定期调用*EvtSerCx2CustomReceiveTransactionQueryProgress*函数来检测回执的第一个字节，并可能需要定期唤醒处理器来进行这些调用。 因此，驱动程序实现*EvtSerCx2CustomReceiveTransactionEnableNewDataNotification*函数可以通过不要求使用处理器而那样频繁地唤醒减少电源消耗。

SerCx2 不会显式取消挂起的新数据通知的自定义接收事务。 但是，串行控制器驱动程序可能需要隐式取消新数据通知，如果启用通知，并且该驱动程序必须完成相关联的读取的请求，出于以下原因之一：

- 读取的请求超时或被取消。
- 串行控制器即将退出 D0 设备电源状态进入低功耗状态。

该驱动程序通常会调用一个方法如[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成该请求。 该驱动程序必须永远不会调用**SerCx2CustomReceiveTransactionNewDataNotification**请求完成后。

## <a name="accessing-the-request-object"></a>访问请求对象

若要开始自定义接收事务，SerCx2 调用驱动程序的[ *EvtSerCx2CustomReceiveTransactionStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_receive_transaction_start)函数并传递关联的读取请求 （封装在 WDFREQUEST 对象处理） 对此函数作为参数。 该驱动程序负责调用一个方法，如[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)若要在事务结束时完成此请求。 除非请求可以完成之前立即*EvtSerCx2CustomReceiveTransactionStart*函数返回时，该驱动程序必须调用方法如[ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)将标记为可取消请求。

串行控制器驱动程序必须使用一种方法诸如[ **WdfRequestRetrieveOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)来访问数据缓冲区中读取的请求。 相反，应使用该驱动程序*Mdl*，*偏移量*，并*长度*参数值传递给*EvtSerCx2CustomReceiveTransactionStart*函数来访问此缓冲区。

在自定义接收事务，该驱动程序可能需要附加到请求对象的上下文中存储事务有关的信息。 如果是这样，驱动程序的[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)事件回调函数可以调用[ **WdfDeviceInitSetRequestAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)方法若要设置要用于请求对象的属性。 这些属性包括要使用的请求上下文的名称和分配大小。 此调用中指定的请求属性必须与匹配对的调用中指定驱动程序的请求属性[ **SerCx2InitializeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2initializedevice)方法。 这些属性中指定**RequestAttributes**的成员**SERCX2\_CONFIG**结构的驱动程序将传递给**SerCx2InitializeDevice**. 有关详细信息，请参阅[ **SERCX2\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_config)。

在开始接收串行控制器驱动程序的读取请求的自定义接收事务、 分配的驱动程序框架的请求上下文未初始化。 该驱动程序应，最佳做法是，调用[ **RtlZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)例程，以初始化为全零此请求上下文。
