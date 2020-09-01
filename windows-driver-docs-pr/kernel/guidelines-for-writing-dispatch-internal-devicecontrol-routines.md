---
title: 有关编写 Dispatch(Internal)DeviceControl 例程的指导原则
description: 有关编写 Dispatch(Internal)DeviceControl 例程的指导原则
ms.assetid: e64ab28e-2904-41c2-a262-405bc129b9bb
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度例程 WDK 内核，DispatchInternalDeviceControl 例程
- DispatchDeviceControl 例程
- DispatchInternalDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL i/o 函数代码
- IRP_MJ_INTERNAL_DEVICE_CONTROL i/o 函数代码
- 内部设备控制调度例程 WDK 内核
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5efeda95989d7e36c8eee8e947e782b810c69e6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183876"
---
# <a name="guidelines-for-writing-dispatchinternaldevicecontrol-routines"></a>有关编写 Dispatch(Internal)DeviceControl 例程的指导原则





编写 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 或 [*DispatchInternalDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程时，请记住以下几点：

至少，更高级别的驱动程序必须将 [**irp \_ mj \_ 设备 \_ 控制**](./irp-mj-device-control.md) 的参数或 [**irp \_ mj \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md) 请求从其自己的 i/o 堆栈位置复制到下一个较低级别的驱动程序的 i/o 堆栈位置。 然后，它必须调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，其中包含指向下一个较低驱动程序的设备对象和 IRP 的指针。

较高级别的驱动程序应传播 **IoCallDriver** 返回的状态值，或在返回的 IRP 的 i/o 状态块中设置此值，以便在返回更低驱动程序处理的请求时进行控制。

基础设备驱动程序必须处理设备控制请求，除非它具有一个紧密耦合类驱动程序，该驱动程序将代表其完成这些请求的一个子集。 设备驱动程序的 *DispatchDeviceControl* 例程通常开始处理这些请求，方法是在每个 IRP 的 i/o 堆栈位置启用 **DeviceIoControl. IoControlCode** 。

较低级别的设备驱动程序应该检查通过请求传入的参数，如果任何参数无效，则将使用适当的错误使 IRP 失败。 对这些请求的参数有效性最常见的检查格式如下：

```cpp
    if (Irp->Parameters.DeviceIoControl.InputBufferLength < 
            (sizeof(IOCTL_SPECIFIC_STRUCTURE))) { 
        status = STATUS_XXX;
```

或
```cpp
    if (Irp->Parameters.DeviceIoControl.OutputBufferLength < 
            (sizeof(IOCTL_SPECIFIC_STRUCTURE))) { 
        status = STATUS_XXX; 
```

其中，status 值集是状态缓冲区之一 \_ \_ 太 \_ 小或状态 \_ 无效 \_ 参数。
每个设备驱动程序的 *DispatchDeviceControl* 或 *DispatchInternalDeviceControl* 例程必须通过使用相应的 NTSTATUS 值设置 i/o 状态块来处理无法识别的 i/o 控制代码，将其 **信息** 字段设置为零，并使用 IO *PriorityBoost* 完成 IRP， \_ 无 \_ 增量。

设备驱动程序句柄的特定 i/o 控制代码必须包含相同类型设备的任何特定于设备类型的、系统定义的 i/o 控制代码。 有关这些 i/o 控制代码的系统定义结构的声明，请参阅 Windows 驱动程序工具包 (WDK) 的设备特定部分，详细了解每种设备类型的系统要求和相应的 (Windows SDK) 头文件，每个文件以前缀 *ntdd*开头。

紧耦合类/端口驱动程序对的类驱动程序可以处理和完成设备控制请求的一个子集，而无需将其传递到基础端口驱动程序。 但是，此类驱动程序必须通过所有需要更改设备状态的有效设备控制请求，以及需要返回有关设备的可变信息（如当前波特率、音量或视频模式）的请求。

 

