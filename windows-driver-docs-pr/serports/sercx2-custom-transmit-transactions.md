---
title: SerCx2 Custom-Transmit 事务
description: 某些串行控制器硬件可能会实现一种数据传输机制，而不是使用 PIO 或系统 DMA 向串行控制器写入数据。
ms.assetid: E72E68BC-A60A-41BE-8606-92A608648042
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef16fa5c356043427279dd218dfa15d55897aa5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843046"
---
# <a name="sercx2-custom-transmit-transactions"></a>SerCx2 Custom-Transmit 事务

某些串行控制器硬件可能会实现一种数据传输机制，而不是使用 PIO 或系统 DMA 向串行控制器写入数据。 串行控制器驱动程序可以支持自定义传输事务，以使 SerCx2 可以使用此数据传输机制。

若要启动自定义传输事务，SerCx2 将调用驱动程序的[*EvtSerCx2CustomTransmitTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)事件回调函数，并将其作为参数提供（[**IRP\_MJ\_写入**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))）请求和描述事务的写入缓冲区。 在此调用中，函数启动事务并返回。 然后，该驱动程序负责完成该事务并完成写入请求。

## <a name="creating-the-custom-transmit-object"></a>创建自定义传输对象

在 SerCx2 可以调用任何串行控制器驱动程序的*EvtSerCx2CustomTransmitTransaction*Xxx * * 函数之前，驱动程序必须调用[**SerCx2CustomTransmitTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)方法将这些函数注册到 SerCx2。 此方法接受作为输入参数的指针，指向[**SERCX2\_自定义\_传输\_的事务\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_custom_transmit_transaction_config)结构，该结构包含指向驱动程序*EvtSerCx2CustomTransmitTransaction*Xxx 的指针 * *函数.

驱动程序必须实现以下函数：

- [*EvtSerCx2CustomTransmitTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)

作为选项，驱动程序可以实现以下一个或两个函数：

- [*EvtSerCx2CustomTransmitTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_initialize)
- [*EvtSerCx2CustomTransmitTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_cleanup)

**SerCx2CustomTransmitTransactionCreate**方法创建自定义传输对象，并向该对象的[**SERCX2CUSTOMTRANSMITTRANSACTION**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles#sercx2customtransmittransaction-object-handle)句柄提供调用驱动程序。 驱动程序的*EvtSerCx2CustomTransmitTransaction*Xxx * * 函数全部使用此句柄作为其第一个参数。 以下 SerCx2 方法使用此句柄作为其第一个参数：

- [**SerCx2CustomTransmitTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioninitializecomplete)
- [**SerCx2CustomTransmitTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncleanupcomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要在自定义传输事务开始时初始化串行控制器硬件，或在事务结束时清理串行控制器的硬件状态。

如果驱动程序实现了[*EvtSerCx2CustomTransmitTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_initialize)事件回调函数，SerCx2 将在启动该事务之前调用此函数以初始化串行控制器。 如果实现，则*EvtSerCx2CustomTransmitTransactionInitialize*函数必须调用[**SerCx2CustomTransmitTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioninitializecomplete)方法，以便在驱动程序完成串行控制器初始化后通知 SerCx2。

如果驱动程序实现了[*EvtSerCx2CustomTransmitTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_cleanup)事件回调函数，SerCx2 将调用此函数以在事务结束后清理硬件状态。 如果实现，则*EvtSerCx2CustomTransmitTransactionInitialize*函数必须调用[**SerCx2CustomTransmitTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncleanupcomplete)方法，以便在驱动程序完成串行控制器清理后通知 SerCx2。

## <a name="accessing-the-request-object"></a>访问请求对象

若要启动自定义传输事务，SerCx2 将调用驱动程序的[*EvtSerCx2CustomTransmitTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)函数，并将关联的写入请求（封装在 WDFREQUEST 对象句柄中）传递给此函数作为参数。 在事务完成时，驱动程序负责调用方法（如[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) ）来完成该请求。 除非可以立即完成请求，否则，驱动程序必须调用方法（如[**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) ）以将请求标记为可取消*EvtSerCx2CustomTransmitTransactionStart* 。

串行控制器驱动程序不得使用[**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)等方法来访问写入请求中的数据缓冲区。 相反，驱动程序应使用传递给*EvtSerCx2CustomTransmitTransactionStart*函数的*Mdl*、 *Offset*和*Length*参数值来访问此缓冲区。

在自定义传输事务期间，驱动程序可能需要在附加到请求对象的上下文中存储有关事务的信息。 如果是这样，驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)事件回调函数可以调用[**WdfDeviceInitSetRequestAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)方法来设置用于请求对象的特性。 这些属性包括用于请求上下文的名称和分配大小。 在此调用中指定的请求属性必须与驱动程序在对[**SerCx2InitializeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2initializedevice)方法的调用中指定的请求属性匹配。 这些属性是在驱动程序传递给**SerCx2InitializeDevice**的**SERCX2\_CONFIG**结构的**RequestAttributes**成员中指定的。 有关详细信息，请参阅[**SERCX2\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_config)。

对于串行控制器驱动程序在自定义传输事务开始时接收的写入请求，驱动程序框架所分配的请求上下文未初始化。 作为最佳方案，驱动程序应调用[**RtlZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)例程将此请求上下文初始化为全部为零。
