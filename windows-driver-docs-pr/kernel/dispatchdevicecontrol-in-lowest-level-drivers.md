---
title: 最低级驱动程序中的 DispatchDeviceControl
description: 最低级驱动程序中的 DispatchDeviceControl
ms.assetid: 51caacd3-c9e0-450e-9060-f308ab46b5a0
keywords:
- 调度例程 WDK 内核，DispatchDeviceControl 例程
- 调度 DispatchDeviceControl 例程
- IRP_MJ_DEVICE_CONTROL I/O 函数代码
- 设备控制调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad687bc8357e6f66806fe260bcd9225cc2eacef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382820"
---
# <a name="dispatchdevicecontrol-in-lowest-level-drivers"></a>最低级驱动程序中的 DispatchDeviceControl





[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求最低级别驱动程序需要的驱动程序将其设备的状态更改或提供的信息有关其设备的状态。 因为大多数类型的驱动程序需要处理大量的 I/O 控制代码，其[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程通常包含**切换**语句某种程度上类似于下面：

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

此代码片段所示，如*DispatchDeviceControl*例程还会检查参数，有时是代表该驱动程序必须支持，有时这些 I/O 控制代码组的每个 I/O 控制代码。

请考虑下面的设备驱动程序的实现指导*DispatchDeviceControl*例程：

-   *DispatchDeviceControl*必须检查的有效性，并立即完成 Irp 参数错误参数中所述[Irp 完成](completing-irps.md)。

-   分组中的 I/O 控制代码**用例**语句 （在实际应用中） 对有效的参数进行测试时驱动程序性能和大小方面，在代码维护经济实惠的方案。 在前面代码片段所示，使用常见的结构的 I/O 控制代码是对这些产品的自然之选**用例**组。

-   切换首先对任何 I/O 控制代码为其*DispatchDeviceControl*例程可以满足和完整 IRP 提高性能，因为该驱动程序可以返回控件更快。

-   切换稍后指定很少的 I/O 控制代码请求的操作还可以提高在处理过程中的驱动程序的性能**IRP\_MJ\_设备\_控制**请求。

-   为了提高性能，每个最低级别的设备驱动程序的*DispatchDeviceControl*例程应满足的任何设备控制请求都可以而无需其他驱动程序例程 IRP 队列。

如果*DispatchDeviceControl*例程可以完成 IRP，应调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与*PriorityBoost*的 IO\_否\_增量。 如果*DispatchDeviceControl*例程必须排队进行进一步处理 IRP，必须调用[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)并返回状态\_PENDING。

 

 




