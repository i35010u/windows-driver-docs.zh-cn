---
title: 将 IRP 调度到 I/O 队列
description: 将 IRP 调度到 I/O 队列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4204d32e8e15c51c7e6c1b80fb784abcb6e71827
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814835"
---
# <a name="dispatching-irps-to-io-queues"></a>将 IRP 调度到 I/O 队列


\[适用于 KMDF 和 UMDF\]

基于框架的驱动程序可以动态指定传入 IRP 的目标队列。 若要将 IRP 分派给特定队列，驱动程序必须调用 [**WdfDeviceWdmDispatchIrpToIoQueue**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 方法。

通常，驱动程序从其 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)或 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)回调函数调用 [**WdfDeviceWdmDispatchIrpToIoQueue**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。 为了获得最佳性能，大多数驱动程序并不提供两个回调函数。

**注意**  UMDF 驱动程序可以提供 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) 回调函数，但只有 KMDF 驱动程序才能提供 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)。

 

如果你的驱动程序已经提供 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)，则可以使用它来动态选择队列。 否则，请提供 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) 并从该回调函数中调用 [**WdfDeviceWdmDispatchIrpToIoQueue**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。

此外，应注意以下事项：

-   将 IRP 调度到 i/o 队列的另一种方法是 [创建一个默认队列](creating-i-o-queues.md) ，然后从该队列的处理程序中调用 [**WdfRequestForwardToIoQueue**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)。 此方法从 KMDF 1.0 开始提供，但无法很好地与 [前进进度队列](guaranteeing-forward-progress-of-i-o-operations.md) 一起使用，并且速度通常较慢。 请考虑改用 [**WdfDeviceWdmDispatchIrpToIoQueue**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 。

-   在调用 [**WdfDeviceConfigureWdmIrpDispatchCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback) 注册 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) 回调函数时，驱动程序必须将 *MajorFunction* 参数设置为以下其中一项： irp \_ mj \_ 设备 \_ 控制、irp MJ \_ \_ 内部 \_ 设备 \_ 控制、irp \_ mj \_ 读取、irp \_ mj \_ 写入。 虽然此要求不适用于 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)，但只能将这些类型的 irp 动态调度到指定的队列。

-   中转到 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 的 irp 具有其他堆栈位置。 无需先前调用 *EvtDeviceWdmIrpPreprocess* 的 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) (的 irp) 。

-   [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 不利于发送驱动程序定义的上下文信息，而 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) 会。

## <a name="dispatching-non-preprocessed-irps"></a>调度非预处理 Irp


若要从驱动程序的 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) 回调函数调度 irp，请使用以下过程：

1.  驱动程序通过其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数调用 [**WdfDeviceConfigureWdmIrpDispatchCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurewdmirpdispatchcallback) 来注册 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) 回调函数。

    如果目标为父设备的 i/o 队列，则 KMDF 驱动程序必须先调用 [**WdfPdoInitAllowForwardingRequestToParent**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent) ，然后才能调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。 如果 KMDF 驱动程序还提供了 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数，则在 IRP 到达时，框架将首先调用该函数。 回调函数预处理请求后，它会调用 [**WdfDeviceWdmDispatchPreprocessedIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchpreprocessedirp) 将 IRP 返回到框架。

2.  框架调用驱动程序的 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch) 回调函数。
3.  从 [*EvtDeviceWdmIrpDispatch*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)中，驱动程序可以调用 [**WdfDeviceWdmDispatchIrpToIoQueue**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) 或 [**WdfDeviceWdmDispatchIrp**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirp)，但不能同时调用两者。 KMDF 驱动程序具有额外的选项，用于调用这两种方法，而是完成 IRP 或将其标记为挂起。
4.  如果 KMDF 驱动程序已将 WDF \_ 调度 \_ IRP 设置 \_ 为 \_ IO \_ 队列 \_ INVOKE \_ INCALLERCTX \_ 回调标志，但没有为目标 i/o 队列启用有保证的前进进度，则框架将调用该驱动程序的 [*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)（如果已提供）。 在对请求进行预处理后，回调函数必须通过调用 [**WdfDeviceEnqueueRequest**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest) 来对其进行排队或通过调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成。

## <a name="dispatching-preprocessed-irps"></a>调度预处理的 Irp


若要将 Irp 从驱动程序的 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess) 回调函数调度到特定 i/o 队列，请使用以下过程：

1.  驱动程序通过调用 [**WdfDeviceInitAssignWdmIrpPreprocessCallback**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)来注册 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数。
2.  如果目标为父设备的 i/o 队列，则驱动程序将调用 [**WdfPdoInitAllowForwardingRequestToParent**](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallowforwardingrequesttoparent) 。
3.  从 [*EvtDeviceWdmIrpPreprocess*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)中，调用 [**WdfDeviceWdmDispatchIrpToIoQueue**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue) ，并将 *标志* 设置为 WDF \_ 调度 \_ irp \_ 到 \_ IO \_ 队列 \_ 预处理 \_ irp。
4.  如果驱动程序已将 WDF \_ 调度 \_ IRP 设置 \_ 为 \_ IO \_ 队列 \_ INVOKE \_ INCALLERCTX \_ 回调标志，并且尚未对目标 i/o 队列启用保证前进进度，则框架将调用该驱动程序的 [*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)（如果已提供）。 回调函数完成预处理请求后，必须通过调用 [**WdfDeviceEnqueueRequest**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest) 或通过调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成请求。

 

