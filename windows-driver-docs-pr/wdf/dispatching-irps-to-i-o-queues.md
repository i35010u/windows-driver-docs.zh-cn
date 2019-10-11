---
title: 将 IRP 调度到 I/O 队列
description: 将 IRP 调度到 I/O 队列
ms.assetid: 71872114-2A38-47FE-9D18-EF8923273811
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b28c4849d0f108858fea7246233de7f08b0f355
ms.sourcegitcommit: 533a5693e8cddb7e19491573ca07ae7b02c2816d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2019
ms.locfileid: "72185542"
---
# <a name="dispatching-irps-to-io-queues"></a>将 IRP 调度到 I/O 队列


\[Applies 到 KMDF 和 UMDF @ no__t-1

基于框架的驱动程序可以动态指定传入 IRP 的目标队列。 若要将 IRP 分派给特定队列，驱动程序必须调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)方法。

通常，驱动程序从其[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)或[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。 为了获得最佳性能，大多数驱动程序并不提供两个回调函数。

**请注意**  a UMDF 驱动程序可提供[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数，但只有 KMDF 驱动程序才能提供[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)。

 

如果你的驱动程序已经提供[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)，则可以使用它来动态选择队列。 否则，请提供[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)并从该回调函数中调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。

此外，应注意以下事项：

-   将 IRP 调度到 i/o 队列的另一种方法是[创建一个默认队列](creating-i-o-queues.md)，然后从该队列的处理程序中调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)。 此方法从 KMDF 1.0 开始提供，但无法很好地与[前进进度队列](guaranteeing-forward-progress-of-i-o-operations.md)一起使用，并且速度通常较慢。 请考虑改用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。

-   在调用[**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)以注册[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数时，驱动程序必须将*MajorFunction*参数设置为以下其中一项：IRP @ NO__T-0MJ @ NO__T-1DEVICE @ NO__T-2CONTROL，IRP @ NO__T-3MJ @ NO__T-4INTERNAL @ NO__T-5DEVICE @ NO__T-6CONTROL，IRP @ NO__T-7MJ @ NO__T-8READ，IRP @ NO__T-9MJ @ NO__T-10WRITE。 虽然此要求不适用于[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)，但只能将这些类型的 irp 动态调度到指定的队列。

-   中转到[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)的 irp 具有其他堆栈位置。 中转到[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) （无需先前调用*EvtDeviceWdmIrpPreprocess*）的 irp 不会。

-   [*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)不利于发送驱动程序定义的上下文信息，而[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)会。

## <a name="dispatching-non-preprocessed-irps"></a>调度非预处理 Irp


若要从驱动程序的[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数调度 irp，请使用以下过程：

1.  驱动程序通过其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用[**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)来注册[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数。

    如果目标为父设备的 i/o 队列，则 KMDF 驱动程序必须先调用[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent) ，然后才能调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)。 如果 KMDF 驱动程序还提供了[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数，则在 IRP 到达时，框架将首先调用该函数。 回调函数预处理请求后，它会调用[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)将 IRP 返回到框架。

2.  框架调用驱动程序的[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数。
3.  从[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)中，驱动程序可以调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)或[**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)，但不能同时调用两者。 KMDF 驱动程序具有额外的选项，用于调用这两种方法，而是完成 IRP 或将其标记为挂起。
4.  如果 KMDF 驱动程序已设置 WDF @ no__t-0DISPATCH @ no__t-1IRP @ no__t-2TO @ no__t-3IO @ no__t-4QUEUE @ no__t-5INVOKE @ no__t-6INCALLERCTX @ no__t-7CALLBACK 标志，并且没有为目标 i/o 队列启用了保证前进进度，则框架将调用驱动程序的[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)（如果已提供）。 在对请求进行预处理后，回调函数必须通过调用[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)来对其进行排队或通过调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成。

## <a name="dispatching-preprocessed-irps"></a>调度预处理的 Irp


若要将 Irp 从驱动程序的[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数调度到特定 i/o 队列，请使用以下过程：

1.  驱动程序通过调用[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)来注册[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数。
2.  如果目标为父设备的 i/o 队列，则驱动程序将调用[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent) 。
3.  在[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)中，调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) ，并将*标志*设置为 WDF @ NO__T-5DISPATCH @ NO__T-6IRP @ NO__T-7TO @ no__t-8IO @ NO__T-9QUEUE @ no__t-10PREPROCESSED @ no__t-11IRP。
4.  如果驱动程序已设置 WDF @ no__t-0DISPATCH @ no__t-1IRP @ no__t-2TO @ no__t-3IO @ no__t-4QUEUE @ no__t-5INVOKE @ no__t-6INCALLERCTX @ no__t-7CALLBACK 标志，并且没有为目标 i/o 队列启用保证前进进度，则框架将调用驱动程序的[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)（如果已提供）。 回调函数完成预处理请求后，必须通过调用[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)或通过调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成请求。

 

 





