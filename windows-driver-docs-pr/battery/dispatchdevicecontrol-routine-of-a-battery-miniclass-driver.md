---
title: 电池微型类驱动程序的 DispatchDeviceControl 例程
description: 电池微型类驱动程序的 DispatchDeviceControl 例程
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- DispatchDeviceControl 例程
- IOCTLs WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34ead5d3881b98182b3b42b5f9fa06d471eba32a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784349"
---
# <a name="dispatchdevicecontrol-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 DispatchDeviceControl 例程


## <span id="ddk_dispatchdevicecontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHDEVICECONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


电源管理器通过复合电池驱动程序将设备控制 Irp (IRP \_ MJ \_ 设备 \_ 控制发送) 到 miniclass 驱动程序。 电池 miniclass 驱动程序中的 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程处理包含电池 IOCTLs 的 irp。

在 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)中，miniclass 驱动程序可以调用类驱动程序的 [**BatteryClassIoctl**](/windows/win32/api/batclass/nf-batclass-batteryclassioctl) 例程来执行任何系统定义的设备控制任务; **BatteryClassIoctl** 处理电池的设备控制 IOCTLs。

[*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程应执行以下操作：

1.  如果 miniclass 驱动程序定义任何专用 IOCTLs，请确定当前 IOCTL 是否在其中。 如果是这样，请执行请求的操作，完成 IRP，指定 IO \_ 无 \_ 增量，并跳到步骤4。

2.  如果 IOCTL 不是由 miniclass 驱动程序定义的专用 IOCTL，请调用 **BatteryClassIoctl**，同时传递 IRP 和 [**BatteryClassInitializeDevice**](/windows/win32/api/batclass/nf-batclass-batteryclassinitializedevice)返回的类句柄。 例如：

    ```cpp
    Status = BatteryClassIoctl (NewBattNP->ClassHandle, Irp);
    ```

    类驱动程序的 [**BatteryClassIoctl**](/windows/win32/api/batclass/nf-batclass-batteryclassioctl)例程确定 IOCTL 是否适用于指定的电池。 如果是这样，它将调用相应的 [BatteryMini *Xxx*](/windows-hardware/drivers/ddi/_battery/)例程来满足请求，然后完成 IRP，返回状态 " \_ 成功"。 否则，它将返回 \_ 不 \_ 受支持的状态。

3.  如果 [**BatteryClassIoctl**](/windows/win32/api/batclass/nf-batclass-batteryclassioctl) 返回 \_ 不 \_ 受支持的状态，指示这不是电池 IRP，请将 IRP 传递到下一个较低的驱动程序。

4.  将返回的状态作为其自己的函数返回值传递。

 

