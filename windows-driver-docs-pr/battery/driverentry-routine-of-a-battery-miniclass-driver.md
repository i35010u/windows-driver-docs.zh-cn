---
title: 电池微型类驱动程序的 DriverEntry 例程
description: 电池微型类驱动程序的 DriverEntry 例程
ms.assetid: dc7c9f75-835b-4646-b30b-24c9dcb6ed2d
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- DriverEntry WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7b25b1095d4e684239912c8e08137f68163d7e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354070"
---
# <a name="driverentry-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 DriverEntry 例程


## <span id="ddk_driverentry_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DRIVERENTRY_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程初始化 miniclass 驱动程序。

Miniclass 驱动[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程将设置以下特定于驱动程序的入口点：

-   [ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程中*DriverObject*-&gt;**DriverUnload**

-   在驱动程序[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程中*DriverObject*-&gt;**DriverExtension** - &gt; **AddDevice**

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)中的回调函数*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)中的回调函数*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)中的回调函数*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)中的回调函数*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)中的回调函数*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)\]

-   [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)中的回调函数*DriverObject*-&gt;**MajorFunction** \[[ **IRP\_MJ\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)\]。

下面的示例代码初始化这些假设 NewBatt miniclass 驱动程序的入口点：

```cpp
DriverObject->DriverUnload = NewBattUnload;
DriverObject->DriverExtension->AddDevice = NewBattAddDevice; 
DriverObject->MajorFunction[IRP_MJ_DEVICE_CONTROL] = NewBattDispatchDeviceControl;
DriverObject->MajorFunction[IRP_MJ_CREATE] = NewBattDispatchCreate;
DriverObject->MajorFunction[IRP_MJ_CLOSE] = NewBattDispatchClose;
DriverObject->MajorFunction[IRP_MJ_PNP] = NewBattDispatchPnp;
DriverObject->MajorFunction[IRP_MJ_POWER] = NewBattDispatchPower;
DriverObject->MajorFunction[IRP_MJ_SYSTEM_CONTROL] = NewBattSystemControl;
```

因为直到 PnP 管理器调用 miniclass 驱动程序的特定于电池的状态信息不知道*AddDevice*例程[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程不初始化此类状态。 在中执行特定于设备的初始化*AddDevice*例程。

其他特定于例程的要求，请参阅以下主题：

[AddDevice 例程的电池 Miniclass 驱动程序](adddevice-routine-of-a-battery-miniclass-driver.md)

[DispatchDeviceControl Routine 电池 Miniclass 驱动程序](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[DispatchSystemControl Routine 电池 Miniclass 驱动程序](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[卸载电池 Miniclass 驱动程序例程](unload-routine-of-a-battery-miniclass-driver.md)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




