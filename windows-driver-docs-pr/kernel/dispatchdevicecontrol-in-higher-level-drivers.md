---
title: 在更高级别的驱动程序中的 DispatchDeviceControl
description: 在更高级别的驱动程序中的 DispatchDeviceControl
ms.assetid: baff49c4-8764-4b65-84f4-ce5e10d51ed2
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度 DispatchDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL I/O 函数代码
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b592c7778b5771b53d0581802b4f98d60111716b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542173"
---
# <a name="dispatchdevicecontrol-in-higher-level-drivers"></a>在更高级别的驱动程序中的 DispatchDeviceControl





通常情况下， [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程的更高级别的驱动程序只需将设置下一步低级驱动程序的 I/O 堆栈位置，将 IRP 传递与[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。 *DispatchDeviceControl*例程很少检查输入 IRP 中参数的有效性，因为假定基础设备驱动程序有更好地了解如何处理每个设备类型特定的 I/O 控制请求。

此通用规则可能的例外是*DispatchDeviceControl*例程的类/端口驱动程序对类驱动程序中。 有关处理设备配对的类/端口驱动程序中的控件请求的详细信息，请参阅[类/端口驱动程序中的调度 （内部） DeviceControl](dispatch-internal-devicecontrol-in-class-port-drivers.md)。

任何新的更高级别的驱动程序不是紧密关联与特定设备驱动程序应只需建立[I/O 堆栈位置](i-o-stack-locations.md)的下一步低级驱动程序并传递[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)上请求进行进一步处理。

设备控制请求通常以同步方式处理。 也就是说，更高级别的驾*DispatchDeviceControl*例程可以经常将控制返回给系统，如下所示：

```cpp
        :    : 
    return IoCallDriver(DeviceObject->NextDeviceObject, Irp);
```

但是，更高级别的驱动程序不能使用上述方法，如果较低的驱动程序可能会返回状态\_PENDING 的此类请求。 在这种情况下，更高级别的驱动程序应调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)注册[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。 当*IoCompletion*调用例程，它可以检查 I/O 状态块，以确定是否 IRP 仍为挂起。 如果是， *IoCompletion*例程可能会重试请求或，可能是，调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)调用之前[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) ，并返回状态\_PENDING。 更高级别的驱动程序必须完成状态 IRP\_PENDING 除非它被称为**IoMarkIrpPending**该 IRP 的第一个。

如果基础设备驱动程序必须处理才能完成该请求从设备传输的数据量，然后更高级别的驱动程序可能会处理此类设备控制请求以异步方式。 也就是说，更高级别的驱动程序可能调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)注册*IoCompletion*例程，传递 IRP 到低级驱动程序，并返回从控件自己*DispatchDeviceControl*例程。

几乎所有系统定义的 I/O 控制代码都需要基础设备驱动程序来传输量不大的数据，通常远远小于页面\_大小量。 作为一般规则，更高级别的驱动程序应处理这些请求以同步方式，如前面的代码片段中所示因为低级驱动程序控制，迅速返回。 也就是说，调用在更高级别的驱动程序的开销*IoCompletion*例程无法弥补的任何其他处理该驱动程序的 IRP 可完成的这种短暂的间隔中。

一个更高级别的驱动程序，会分配与 Irp [ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)为基础的设备驱动程序可以处理这些设备控制请求以同步方式。 更高级别的驱动程序可以等待一个可选的事件对象传递给**IoBuildDeviceIoControlRequest**和与驱动程序分配 IRP 相关联。

 

 




