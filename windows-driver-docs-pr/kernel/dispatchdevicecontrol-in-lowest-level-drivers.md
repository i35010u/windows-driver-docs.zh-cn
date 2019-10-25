---
title: 最低级驱动程序中的 DispatchDeviceControl
description: 最低级驱动程序中的 DispatchDeviceControl
ms.assetid: 51caacd3-c9e0-450e-9060-f308ab46b5a0
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度 DispatchDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL i/o 函数代码
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6a872bc8549c12482f4089dd09855ad609b8c42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836866"
---
# <a name="dispatchdevicecontrol-in-lowest-level-drivers"></a>最低级驱动程序中的 DispatchDeviceControl





[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求最低级别的驱动程序要求驱动程序更改设备的状态，或者提供有关设备状态的信息。 由于大多数类型的驱动程序都需要处理多个 i/o 控制代码，因此它们的[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程通常包含如下所示的**switch**语句：

```cpp
    :    : 
switch (irpSp->Parameters.DeviceIoControl.IoControlCode)
{ 
    case IOCTL_DeviceType_XXX: 
    case IOCTL_DeviceType_YYY: 
        if (irpSp->Parameters.DeviceIoControl.InputBufferLength < 
                (sizeof(IOCTL_XXXYYY_STRUCTURE)))
        { 
            status = STATUS_BUFFER_TOO_SMALL; 
            break; 
        } else { 
            IoMarkIrpPending(Irp); 
     :    : // pass IRP on for further processing 
    case ... 
     :    :
```

如下面的代码片段所示， *DispatchDeviceControl*例程还会检查参数，有时会检查驱动程序必须支持的每个 i/o 控制代码（有时是这些 i/o 控制代码的组）。

请考虑以下设备驱动程序的*DispatchDeviceControl*例程实现准则：

-   *DispatchDeviceControl*必须检查参数的有效性，并立即用参数错误完成 irp，如[完成 irp](completing-irps.md)中所述。

-   在用例语句中对 i/o 控制代码进行分组时（在实际**情况下**），在驱动程序的性能、大小和代码维护方面，对有效参数进行的测试非常经济。 如前面的代码片段所示，使用公共结构的 i/o 控制代码是此类**事例**组的自然候选项。

-   在*DispatchDeviceControl*例程可满足并完成 IRP 的任何 i/o 控制代码上首先切换会提高性能，因为驱动程序可以更快地返回控制。

-   稍后切换到指定不常请求的操作的 i/o 控制代码还可以提高驱动程序在处理**IRP\_MJ\_设备\_控制**请求时的性能。

-   为了获得更好的性能，每个最低级别设备驱动程序的*DispatchDeviceControl*例程应满足任何设备控制请求，而不会将 IRP 排队到其他驱动程序例程。

如果*DispatchDeviceControl*例程可以完成 IRP，则应使用 IO *PriorityBoost*调用[**IOCOMPLETEREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，\_没有\_增量。 如果*DispatchDeviceControl*例程必须将 IRP 排队以便进一步处理，则它必须调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)并返回状态\_"挂起"。

 

 




