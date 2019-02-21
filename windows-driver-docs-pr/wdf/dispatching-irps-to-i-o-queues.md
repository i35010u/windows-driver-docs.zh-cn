---
title: 调度到的 I/O 队列的 Irp
description: 调度到的 I/O 队列的 Irp
ms.assetid: 71872114-2A38-47FE-9D18-EF8923273811
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3cbd7dfb6cfb9238d6f1bc37c04dbe5f3f2b783
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524436"
---
# <a name="dispatching-irps-to-io-queues"></a>调度到的 I/O 队列的 Irp


\[适用于 KMDF 和 UMDF\]

基于框架的驱动程序动态可以传入 IRP 为指定的目标队列。 若要调度到特定队列 IRP，驱动程序必须调用[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)方法。

通常情况下，驱动程序调用[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)从其[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)或[*EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调函数。 为了获得最佳性能，大多数驱动程序不提供这两个回调函数。

**请注意**  UMDF 驱动程序可以提供[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调函数，但仅 KMDF 驱动程序可以提供[ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)。

 

如果您的驱动程序已经提供了[ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)，可以使用该队列中动态选择。 如果没有，请提供[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404) ，并调用[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)从该回调函数。

此外，您应注意以下内容：

-   用于调度到的 I/O 队列 IRP 另一种方法是向[创建的默认队列](creating-i-o-queues.md)，然后从该队列的处理程序内调用[ **WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958)。 此方法可以开始于 KMDF 1.0 但不能正常处理[转发进度队列](guaranteeing-forward-progress-of-i-o-operations.md)和在常规速度较慢。 请考虑使用[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)相反。

-   调用时[ **WdfDeviceConfigureWdmIrpDispatchCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh451093)注册[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调函数该驱动程序必须设置*MajorFunction*参数为以下值之一：IRP\_MJ\_设备\_控件、 IRP\_MJ\_内部\_设备\_控件、 IRP\_MJ\_读取、 IRP\_MJ\_编写。 虽然此要求不适用于[ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)、 仅 Irp 的这些类型可以进行动态调度到指定的队列。

-   请转到 Irp [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)具有附加的堆栈位置。 请转到 Irp [ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404) (而无需在前一个调用的*EvtDeviceWdmIrpPreprocess*) 不这样做。

-   [*EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)并不促成发送驱动程序定义的上下文信息，而[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404) does。

## <a name="dispatching-non-preprocessed-irps"></a>调度非预处理过的 Irp


若要从驱动程序的调度 Irp [ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调函数中，使用以下过程：

1.  从其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数、 驱动程序调用[ **WdfDeviceConfigureWdmIrpDispatchCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh451093)到注册[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调函数。

    如果目标是父设备的 I/O 队列，必须调用 KMDF 驱动程序[ **WdfPdoInitAllowForwardingRequestToParent** ](https://msdn.microsoft.com/library/windows/hardware/ff548789)调用之前[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926). 如果 KMDF 驱动程序还提供了[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数，框架将调用该函数首先 IRP 到达时。 回调函数对请求进行预处理后，它会调用[ **WdfDeviceWdmDispatchPreprocessedIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546927)返回 IRP 到框架。

2.  框架将调用的驱动程序[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调函数。
3.  从内部[ *EvtDeviceWdmIrpDispatch*](https://msdn.microsoft.com/library/windows/hardware/hh406404)，该驱动程序可以调用[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)或[ **WdfDeviceWdmDispatchIrp**](https://msdn.microsoft.com/library/windows/hardware/hh451100)，但不可同时使用两者。 KMDF 驱动程序包含调用这两个方法，而是完成 IRP 或将其挂起的标记的其他选项。
4.  如果 KMDF 驱动程序已设置了 WDF\_向前\_IRP\_TO\_IO\_队列\_INVOKE\_INCALLERCTX\_回调标志并启用了不保证对于目标 I/O 队列，然后在 framework 向前推进调用驱动程序的[ *EvtIoInCallerContext*](https://msdn.microsoft.com/library/windows/hardware/ff541764)，如果提供。 在预处理后请求，回调函数必须也在队列中通过调用[ **WdfDeviceEnqueueRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff545945)或通过调用完成[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945).

## <a name="dispatching-preprocessed-irps"></a>调度预处理过的 Irp


若要从驱动程序的调度 Irp [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数到特定的 I/O 队列，请执行以下步骤：

1.  驱动程序寄存器[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)通过调用回调函数[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043).
2.  驱动程序调用[ **WdfPdoInitAllowForwardingRequestToParent** ](https://msdn.microsoft.com/library/windows/hardware/ff548789)如果目标是父设备的 I/O 队列。
3.  从[ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)，调用[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)与*标志*设置为 WDF\_向前\_IRP\_TO\_IO\_队列\_预处理过\_IRP。
4.  如果驱动程序已设置了 WDF\_向前\_IRP\_TO\_IO\_队列\_INVOKE\_INCALLERCTX\_回调标志并启用了不能保证向前对于目标 I/O 队列，然后该框架进行调用的驱动程序[ *EvtIoInCallerContext*](https://msdn.microsoft.com/library/windows/hardware/ff541764)，如果提供。 回调函数完成预处理请求后，它必须或者在队列中通过调用[ **WdfDeviceEnqueueRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff545945)或通过调用完成[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)。

 

 





