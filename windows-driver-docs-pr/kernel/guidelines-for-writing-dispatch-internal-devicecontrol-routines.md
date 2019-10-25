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
ms.openlocfilehash: f05993e9bad112784cbf27352986328fde22fc96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836678"
---
# <a name="guidelines-for-writing-dispatchinternaldevicecontrol-routines"></a>有关编写 Dispatch(Internal)DeviceControl 例程的指导原则





编写[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)或[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程时，请记住以下几点：

更高级别的驱动程序必须至少复制 Irp 的参数[ **\_mj\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)或 IRP\_MJ\_从其自己的 i/o 堆栈位置到 IRP 的[**内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求下一级驱动程序的 i/o 堆栈位置。 然后，它必须调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，其中包含指向下一个较低驱动程序的设备对象和 IRP 的指针。

较高级别的驱动程序应传播**IoCallDriver**返回的状态值，或在返回的 IRP 的 i/o 状态块中设置此值，以便在返回更低驱动程序处理的请求时进行控制。

基础设备驱动程序必须处理设备控制请求，除非它具有一个紧密耦合类驱动程序，该驱动程序将代表其完成这些请求的一个子集。 设备驱动程序的*DispatchDeviceControl*例程通常开始处理这些请求，方法是在每个 IRP 的 i/o 堆栈位置启用**DeviceIoControl. IoControlCode** 。

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

其中，status 值集是状态\_缓冲区之一\_太\_小或状态\_无效的\_参数。
每个设备驱动程序的*DispatchDeviceControl*或*DispatchInternalDeviceControl*例程必须通过使用相应的 NTSTATUS 值设置 i/o 状态块来处理无法识别的 i/o 控制代码，并将其**信息**字段为零，并使用*PRIORITYBOOST*的 IO 完成 IRP\_没有\_递增。

设备驱动程序句柄的特定 i/o 控制代码必须包含相同类型设备的任何特定于设备类型的、系统定义的 i/o 控制代码。 请参阅 Windows 驱动程序工具包（WDK）的设备特定部分，详细了解每种设备的系统要求和对应的（Windows SDK）头文件（每个文件以前缀*ntdd*开头），以供声明这些 i/o 控制代码的系统定义结构。

紧耦合类/端口驱动程序对的类驱动程序可以处理和完成设备控制请求的一个子集，而无需将其传递到基础端口驱动程序。 但是，此类驱动程序必须通过所有需要更改设备状态的有效设备控制请求，以及需要返回有关设备的可变信息（如当前波特率、音量或视频模式）的请求。

 

 




