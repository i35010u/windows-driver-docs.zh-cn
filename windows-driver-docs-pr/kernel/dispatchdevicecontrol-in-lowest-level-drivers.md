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
ms.openlocfilehash: a4f6e5b48e77a7f00a7bf809bb8f71acc715e083
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192721"
---
# <a name="dispatchdevicecontrol-in-lowest-level-drivers"></a>最低级驱动程序中的 DispatchDeviceControl





对于最低级别的驱动程序， [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求需要驱动程序更改其设备的状态，或者提供有关其设备状态的信息。 由于大多数类型的驱动程序都需要处理多个 i/o 控制代码，因此它们的 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程通常包含如下所示的 **switch** 语句：

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

如下面的代码片段所示， *DispatchDeviceControl* 例程还会检查参数，有时会检查驱动程序必须支持的每个 i/o 控制代码（有时是这些 i/o 控制代码的组）。

请考虑以下设备驱动程序的 *DispatchDeviceControl* 例程实现准则：

-   *DispatchDeviceControl* 必须检查参数的有效性，并立即用参数错误完成 irp，如 [完成 irp](completing-irps.md)中所述。

-   在 case 语句中对 i/o 控制代码进行分组 (在某些 **情况下** ，测试有效参数的实际) 在驱动程序性能、大小和代码维护方面非常经济。 如前面的代码片段所示，使用公共结构的 i/o 控制代码是此类 **事例** 组的自然候选项。

-   在 *DispatchDeviceControl* 例程可满足并完成 IRP 的任何 i/o 控制代码上首先切换会提高性能，因为驱动程序可以更快地返回控制。

-   稍后切换到指定不常请求的操作的 i/o 控制代码还可以改善驱动程序在处理 **IRP \_ MJ \_ 设备 \_ 控制** 请求时的性能。

-   为了获得更好的性能，每个最低级别设备驱动程序的 *DispatchDeviceControl* 例程应满足任何设备控制请求，而不会将 IRP 排队到其他驱动程序例程。

如果 *DispatchDeviceControl* 例程可以完成 IRP，则它应调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，而不是 IO 的 *PriorityBoost* \_ \_ 。 如果 *DispatchDeviceControl* 例程必须将 IRP 排队以便进一步处理，则必须调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 并返回状态 " \_ 挂起"。

 

