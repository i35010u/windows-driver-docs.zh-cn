---
title: SerCx2 Custom-Transmit 事务
description: 某些串行控制器硬件可能会实现用于将数据写入串行控制器 PIO 或系统 DMA 以外的数据传输机制。
ms.assetid: E72E68BC-A60A-41BE-8606-92A608648042
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37f8e72759937c97b1a281279ed43c5c4fe5e5f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356786"
---
# <a name="sercx2-custom-transmit-transactions"></a>SerCx2 Custom-Transmit 事务

某些串行控制器硬件可能会实现用于将数据写入串行控制器 PIO 或系统 DMA 以外的数据传输机制。 串行控制器驱动程序支持自定义传输的事务以 SerCx2 即可使用此数据传输机制。

若要开始自定义传输的事务，SerCx2 调用驱动程序的[ *EvtSerCx2CustomTransmitTransactionStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)事件回调函数并作为参数提供对写入 ([ **IRP\_MJ\_编写**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) 请求和事务写入缓冲区的说明。 在此调用中，该函数启动事务，并返回。 然后，该驱动程序是负责完成该事务并完成写入请求。

## <a name="creating-the-custom-transmit-object"></a>创建 custom-transmit 对象

SerCx2 可以调用任何串行控制器驱动程序之前*EvtSerCx2CustomTransmitTransaction*Xxx * * 函数，该驱动程序必须调用[ **SerCx2CustomTransmitTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioncreate)方法以向 SerCx2 注册这些函数。 此方法接受，作为输入参数，一个指向[ **SERCX2\_自定义\_传输\_事务\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_custom_transmit_transaction_config)结构包含的驱动程序的指针*EvtSerCx2CustomTransmitTransaction*Xxx * * 函数。

该驱动程序必须实现以下函数：

- [*EvtSerCx2CustomTransmitTransactionStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)

作为一个选项，该驱动程序可以实现一个或两个以下函数：

- [*EvtSerCx2CustomTransmitTransactionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_initialize)
- [*EvtSerCx2CustomTransmitTransactionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_cleanup)

**SerCx2CustomTransmitTransactionCreate**方法创建 custom-transmit 对象，并提供与调用驱动程序[ **SERCX2CUSTOMTRANSMITTRANSACTION** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles#sercx2customtransmittransaction-object-handle)此对象的句柄。 在驱动程序*EvtSerCx2CustomTransmitTransaction*Xxx * * 函数所有采用该句柄作为其第一个参数。 以下 SerCx2 方法将此句柄作为其第一个参数：

- [**SerCx2CustomTransmitTransactionInitializeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioninitializecomplete)
- [**SerCx2CustomTransmitTransactionCleanupComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioncleanupcomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

某些串行控制器驱动程序可能需要初始化的开头的串行控制器硬件自定义传输的事务，或清除该事务结束时的串行控制器的硬件状态。

如果驱动程序实现[ *EvtSerCx2CustomTransmitTransactionInitialize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_initialize)事件回调函数，SerCx2 调用此函数可初始化之前启动的事务执行串行控制器. 如果实现，则*EvtSerCx2CustomTransmitTransactionInitialize*函数必须调用[ **SerCx2CustomTransmitTransactionInitializeComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioninitializecomplete)方法初始化串行控制器驱动程序完成时通知 SerCx2。

如果该驱动程序实现[ *EvtSerCx2CustomTransmitTransactionCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_cleanup)事件回调函数，SerCx2 调用此函数可在事务结束后清理硬件状态。 如果实现，则*EvtSerCx2CustomTransmitTransactionInitialize*函数必须调用[ **SerCx2CustomTransmitTransactionCleanupComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioncleanupcomplete)方法通知 SerCx2 清理串行控制器驱动程序完成。

## <a name="accessing-the-request-object"></a>访问请求对象

若要开始自定义传输的事务，SerCx2 调用驱动程序的[ *EvtSerCx2CustomTransmitTransactionStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_custom_transmit_transaction_start)函数，并将关联的写入请求 （封装在 WDFREQUEST 传递对象句柄） 对此函数作为参数。 该驱动程序负责调用一个方法，如[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)若要在事务结束时完成此请求。 除非请求可以完成之前立即*EvtSerCx2CustomTransmitTransactionStart*函数返回时，该驱动程序必须调用方法如[ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)将标记为可取消请求。

串行控制器驱动程序必须使用一种方法诸如[ **WdfRequestRetrieveInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)来访问数据缓冲区中写入请求。 相反，应使用该驱动程序*Mdl*，*偏移量*，并*长度*参数值传递给*EvtSerCx2CustomTransmitTransactionStart*函数来访问此缓冲区。

在自定义传输的事务，该驱动程序可能需要附加到请求对象的上下文中存储有关事务的信息。 如果是这样，驱动程序的[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)事件回调函数可以调用[ **WdfDeviceInitSetRequestAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)方法若要设置要用于请求对象的属性。 这些属性包括要使用的请求上下文的名称和分配大小。 此调用中指定的请求属性必须与匹配对的调用中指定驱动程序的请求属性[ **SerCx2InitializeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2initializedevice)方法。 这些属性中指定**RequestAttributes**的成员**SERCX2\_CONFIG**结构的驱动程序将传递给**SerCx2InitializeDevice**. 有关详细信息，请参阅[ **SERCX2\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_config)。

对于串行控制器驱动程序收到的开头写入请求自定义传输的事务，分配的驱动程序框架的请求上下文未初始化。 该驱动程序应，最佳做法是，调用[ **RtlZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)例程，以初始化为全零此请求上下文。
