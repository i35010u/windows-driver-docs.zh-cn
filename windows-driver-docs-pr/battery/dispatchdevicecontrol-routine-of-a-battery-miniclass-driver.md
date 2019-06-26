---
title: 电池微型类驱动程序的 DispatchDeviceControl 例程
description: 电池微型类驱动程序的 DispatchDeviceControl 例程
ms.assetid: 26313dcc-9f37-4c5e-a21e-c4d8a50ff564
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- DispatchDeviceControl 例程
- Ioctl WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8722a72068dc2af185e70a2db6b468cf1dfdc3dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354076"
---
# <a name="dispatchdevicecontrol-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 DispatchDeviceControl 例程


## <span id="ddk_dispatchdevicecontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHDEVICECONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


电源管理器将设备控件 Irp 发送 (IRP\_MJ\_设备\_控件) miniclass 驱动程序通过复合电池驱动程序。 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)电池 miniclass 驱动程序中的例程处理 Irp 包含电池 Ioctl。

在中[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，miniclass 驱动程序可以调用的类驱动程序[ **BatteryClassIoctl** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)例程，以执行任何系统定义的设备控制任务;**BatteryClassIoctl**处理设备控制 Ioctl 的电池。

[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程应执行以下操作：

1.  如果 miniclass 驱动程序定义了任何专用 Ioctl，确定当前 IOCTL 是在它们之间。 如果是这样，执行请求的操作，完成 IRP，指定 IO\_否\_递增，并转到步骤 4。

2.  如果 IOCTL 不是由 miniclass 驱动程序定义专用 IOCTL，调用**BatteryClassIoctl**，将 IRP 和返回的类句柄传递[ **BatteryClassInitializeDevice** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassinitializedevice). 例如：

    ```cpp
    Status = BatteryClassIoctl (NewBattNP->ClassHandle, Irp);
    ```

    在类驱动程序[ **BatteryClassIoctl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)例程确定 IOCTL 是否适用于指定的电池。 如果是，它调用的相应[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_battery/)例程来满足请求，然后完成 IRP，返回状态\_成功。 否则，它将返回状态\_不\_受支持。

3.  如果[ **BatteryClassIoctl** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)返回状态\_不\_支持，，，该值指示这不电池 IRP，将 IRP 传递给下一个较低驱动程序。

4.  将返回的状态作为其自身函数返回值传递。

 

 




