---
title: 较高级驱动程序中的 DispatchDeviceControl
description: 较高级驱动程序中的 DispatchDeviceControl
ms.assetid: baff49c4-8764-4b65-84f4-ce5e10d51ed2
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度 DispatchDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL i/o 函数代码
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7521fc49dadb9ffc54e1598898a071e29f1a27bf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186459"
---
# <a name="dispatchdevicecontrol-in-higher-level-drivers"></a>较高级驱动程序中的 DispatchDeviceControl





通常，较高级别的驱动程序的 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程只是为下一个较低级别的驱动程序设置 i/o 堆栈位置，并将 IRP 传递到 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。 *DispatchDeviceControl*例程很少检查输入 IRP 中参数的有效性，因为假定基础设备驱动程序具有有关如何处理每个特定于设备类型的 i/o 控制请求的更详细信息。

此常规规则的一个可能例外是类/端口驱动程序对的类驱动程序中的 *DispatchDeviceControl* 例程。 有关在成对类/端口驱动程序中处理设备控制请求的详细信息，请参阅 [在类/端口驱动程序中调度 (内部) DeviceControl](dispatch-internal-devicecontrol-in-class-port-drivers.md)。

任何不与特定设备驱动程序紧密关联的高级驱动程序都应该只是为下一个较低级别的驱动程序设置 [i/o 堆栈位置](i-o-stack-locations.md) ，并将 [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求传递到以进行进一步处理。

设备控制请求通常是同步处理的。 也就是说，更高级别的驱动程序的 *DispatchDeviceControl* 例程可以频繁地按如下方式将控制返回给系统：

```cpp
        :    : 
    return IoCallDriver(DeviceObject->NextDeviceObject, Irp);
```

但是，如果低级驱动程序可能会 \_ 针对此类请求返回状态 "挂起"，则较高级别的驱动程序无法使用上述方法。 在这种情况下，较高级别的驱动程序应调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 来注册 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 调用 *IoCompletion* 例程时，它可以检查 i/o 状态块，以确定 IRP 是否仍处于挂起状态。 如果是， *IoCompletion*例程可能会重试请求，或者可能在调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)之前调用[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，并返回状态 " \_ 挂起"。 较高级别的驱动程序不得完成状态为 "已挂起" 的 IRP， \_ 除非它首先为该 irp 调用了 **也** 。

如果基础设备驱动程序在完成请求之前必须处理从设备传输的大量数据，则较高级别的驱动程序可能会以异步方式处理此类设备控制请求。 也就是说，较高级别的驱动程序可以调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 来注册 *IoCompletion* 例程，将 IRP 传递到较低的驱动程序，并从其自己的 *DispatchDeviceControl* 例程返回控制权。

几乎所有系统定义的 i/o 控制代码都要求基础设备驱动程序只传输适度数量的数据，通常远远小于页面 \_ 大小。 作为一般规则，更高级别的驱动程序应同步处理这些请求，如前面的代码片段中所示，因为较低的驱动程序返回控件的速度很快。 也就是说，调用较高级别的驱动程序的 *IoCompletion* 例程的开销不会对该驱动程序可在较短时间间隔内完成的任何其他 IRP 处理进行补偿。

使用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 为基础设备驱动程序分配 irp 的更高级别驱动程序可以同步处理这些设备控制请求。 较高级别的驱动程序可以等待一个可选的事件对象传递给 **IoBuildDeviceIoControlRequest** ，并将其与已分配给驱动程序的 IRP 关联。

 

