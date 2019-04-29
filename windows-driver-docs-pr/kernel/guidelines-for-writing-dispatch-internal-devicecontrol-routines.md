---
title: 有关编写 Dispatch(Internal)DeviceControl 例程的指导原则
description: 有关编写 Dispatch(Internal)DeviceControl 例程的指导原则
ms.assetid: e64ab28e-2904-41c2-a262-405bc129b9bb
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度例程 WDK 内核，DispatchInternalDeviceControl 例程
- DispatchDeviceControl 例程
- DispatchInternalDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL I/O 函数代码
- IRP_MJ_INTERNAL_DEVICE_CONTROL I/O 函数代码
- 内部设备控制调度例程 WDK 内核
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 588966e1a0767a9201345d00cf6205d833bd9e51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359879"
---
# <a name="guidelines-for-writing-dispatchinternaldevicecontrol-routines"></a>有关编写 Dispatch(Internal)DeviceControl 例程的指导原则





编写时记住以下几点[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)或[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程：

更高级别的驱动程序必须在最低限度上，复制的参数[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)或[ **IRP\_MJ\_内部\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550766)从其自己的 I/O 堆栈位置中 IRP 到下一步低级驱动程序的 I/O 堆栈位置请求。 然后，它必须调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)用一个指针指向下一步低驱动程序的设备对象和 IRP。

更高级别的驱动程序应传播由返回的状态值**IoCallDriver**或返回控件的低级驱动程序以同步方式处理的请求时返回的 IRP I/O 状态块中设置。

基础设备驱动程序必须处理设备控制请求，除非它具有的紧密耦合的类驱动程序，完成这些请求代表其自身的子集。 设备驱动程序*DispatchDeviceControl*例程通常会开始处理这些请求通过开启**Parameters.DeviceIoControl.IoControlCode**中其 I/O 堆栈的每个 IRP 的位置。

较低级别设备驱动程序应检查参数随请求传入，并且如果任何参数无效，则失败 IRP 因相应的错误。 这些请求的参数的有效性的最常见检查采用以下格式：

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

其中状态的值设置为状态之一\_缓冲区\_过\_小型或状态\_无效\_参数。
每个设备驱动程序*DispatchDeviceControl*或*DispatchInternalDeviceControl*例程必须通过设置 I/O 状态块包含处理无法识别的 I/O 控制代码的回执适当的 NTSTATUS 值，设置其**信息**字段为零，并完成与 IRP *PriorityBoost*的 IO\_否\_增量。

设备驱动程序处理的特定 I/O 控制代码必须包含相同类型的设备的任何设备类型特定的系统定义的 I/O 控制代码。 请参阅特定于设备的部分详细了解每种类型的设备和相应 (Windows SDK) 标头文件，每个前缀开头的系统要求的 Windows Driver Kit (WDK) *ntdd*，为这些 I/O 控制代码的系统定义结构的声明。

紧密耦合的类/端口驱动程序对在类驱动程序可以处理和完成而无需将它们传递到基础端口驱动程序的设备控制请求的子集。 但是，这样的类驱动程序必须通过在设备和要求的设备，如其当前的波特率、 卷或视频模式的易失性信息返回的那些需要状态更改的所有有效的设备控制请求。

 

 




