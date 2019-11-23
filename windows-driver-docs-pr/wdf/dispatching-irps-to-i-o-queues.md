---
title: 将 IRP 调度到 I/O 队列
description: 将 IRP 调度到 I/O 队列
ms.assetid: 71872114-2A38-47FE-9D18-EF8923273811
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53d42ba9784373a7a2e61010b8fc55604987fe83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845278"
---
# <a name="dispatching-irps-to-io-queues"></a>将 IRP 调度到 I/O 队列


\[适用于 KMDF 和 UMDF\]

基于框架的驱动程序可以动态指定传入 IRP 的目标队列。 若要将 IRP 分派给特定队列，驱动程序必须调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)方法。

通常，驱动程序从其[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)或[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。 为了获得最佳性能，大多数驱动程序并不提供两个回调函数。

**请注意**  UMDF 驱动程序可以提供[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数，但只有 KMDF 驱动程序才能提供[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)。

 

如果你的驱动程序已经提供[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)，则可以使用它来动态选择队列。 否则，请提供[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)并从该回调函数中调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。

此外，应注意以下事项：

-   将 IRP 调度到 i/o 队列的另一种方法是[创建一个默认队列](creating-i-o-queues.md)，然后从该队列的处理程序中调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)。 此方法从 KMDF 1.0 开始提供，但无法很好地与[前进进度队列](guaranteeing-forward-progress-of-i-o-operations.md)一起使用，并且速度通常较慢。 请考虑改用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。

-   在调用[**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)以注册[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数时，驱动程序必须将*MajorFunction*参数设置为以下其中一项： IRP\_MJ\_设备\_控制、IRP\_MJ\_内部\_设备\_控制、irp\_\_\_\_ 虽然此要求不适用于[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)，但只能将这些类型的 irp 动态调度到指定的队列。

-   中转到[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)的 irp 具有其他堆栈位置。 中转到[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) （无需先前调用*EvtDeviceWdmIrpPreprocess*）的 irp 不会。

-   [*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)不利于发送驱动程序定义的上下文信息，而[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)会。

## <a name="dispatching-non-preprocessed-irps"></a>调度非预处理 Irp


若要从驱动程序的[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数调度 irp，请使用以下过程：

1.  驱动程序通过其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用[**WdfDeviceConfigureWdmIrpDispatchCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback)来注册[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数。

    如果目标为父设备的 i/o 队列，则 KMDF 驱动程序必须先调用[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent) ，然后才能调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。 如果 KMDF 驱动程序还提供了[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数，则在 IRP 到达时，框架将首先调用该函数。 回调函数预处理请求后，它会调用[**WdfDeviceWdmDispatchPreprocessedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp)将 IRP 返回到框架。

2.  框架调用驱动程序的[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数。
3.  从[*EvtDeviceWdmIrpDispatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)中，驱动程序可以调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)或[**WdfDeviceWdmDispatchIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)，但不能同时调用两者。 KMDF 驱动程序具有额外的选项，用于调用这两种方法，而是完成 IRP 或将其标记为挂起。
4.  如果 KMDF 驱动程序已设置 WDF\_调度\_IRP\_到\_IO\_QUEUE\_调用\_INCALLERCTX\_回调标志，并且没有为目标 i/o 队列启用有保证的前进进度，则框架将调用该驱动程序的[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)（如果已提供）。 在对请求进行预处理后，回调函数必须通过调用[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)来对其进行排队或通过调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成。

## <a name="dispatching-preprocessed-irps"></a>调度预处理的 Irp


若要将 Irp 从驱动程序的[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数调度到特定 i/o 队列，请使用以下过程：

1.  驱动程序通过调用[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)来注册[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数。
2.  如果目标为父设备的 i/o 队列，则驱动程序将调用[**WdfPdoInitAllowForwardingRequestToParent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent) 。
3.  在[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)中，通过将*标志*设置为 WDF 来调用[**WdfDeviceWdmDispatchIrpToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)\_调度\_IRP\_\_IO\_QUEUE\_预处理\_IRP。
4.  如果驱动程序已设置 WDF\_调度\_IRP\_到\_IO\_QUEUE\_调用\_INCALLERCTX\_回调标志，并且没有为目标 i/o 队列启用有保证的前进进度，则框架将调用驱动程序的[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)（如果已提供）。 回调函数完成预处理请求后，必须通过调用[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)或通过调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成请求。

 

 





