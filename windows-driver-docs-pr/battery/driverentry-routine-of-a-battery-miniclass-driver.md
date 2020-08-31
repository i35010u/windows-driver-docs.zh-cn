---
title: 电池微型类驱动程序的 DriverEntry 例程
description: 电池微型类驱动程序的 DriverEntry 例程
ms.assetid: dc7c9f75-835b-4646-b30b-24c9dcb6ed2d
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- DriverEntry WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 607a9c76e0ef96c8c94da0be3b4c19d437e41691
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056909"
---
# <a name="driverentry-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 DriverEntry 例程


## <span id="ddk_driverentry_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DRIVERENTRY_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


[*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程初始化 miniclass 驱动程序。

Miniclass 驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程设置以下特定于驱动程序的入口点：

-   [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) *DriverObject* - &gt; **DriverUnload**中的 Unload 例程

-   [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) *DriverObject* - &gt; **DriverExtension** - &gt; **AddDevice**中的驱动程序的 AddDevice 例程

-   [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) *DriverObject* - &gt; **MajorFunction** \[ [**IRP \_ MJ \_ POWER**](../kernel/irp-mj-power.md)中的 DRIVER_DISPATCH 回调函数\]

-   [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) *DriverObject* - &gt; **MajorFunction** \[ [**IRP \_ MJ \_ PNP**](../kernel/irp-mj-pnp.md)中的 DRIVER_DISPATCH 回调函数\]

-   [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) *DriverObject* - &gt; **MajorFunction** \[ [**IRP \_ MJ \_ CREATE**](../kernel/irp-mj-create.md)中的 DRIVER_DISPATCH 回调函数\]

-   [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) *DriverObject* - &gt; **MajorFunction** \[ [**IRP \_ MJ \_ CLOSE**](../kernel/irp-mj-close.md)中的 DRIVER_DISPATCH 回调函数\]

-   [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) *DriverObject* - &gt; **MajorFunction** \[ [**IRP \_ MJ \_ 设备 \_ 控件**](../kernel/irp-mj-device-control.md)中的 DRIVER_DISPATCH 回调函数\]

-   [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) *DriverObject* - &gt; **MajorFunction** \[ [**IRP \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)中的 DRIVER_DISPATCH 回调函数 \] 。

下面的示例代码为假设的 NewBatt miniclass 驱动程序初始化这些入口点：

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

由于在 PnP 管理器调用 miniclass 驱动程序的 *AddDevice* 例程之前，特定于电池的状态信息是未知的，因此 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程不会初始化任何此类状态。 特定于设备的初始化是在 *AddDevice* 例程中执行的。

有关其他特定于例程的要求，请参阅以下主题：

[电池微型类驱动程序的 AddDevice 例程](adddevice-routine-of-a-battery-miniclass-driver.md)

[电池微型类驱动程序的 DispatchDeviceControl 例程](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[电池微型类驱动程序的 DispatchSystemControl 例程](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[电池微型类驱动程序的 Unload 例程](unload-routine-of-a-battery-miniclass-driver.md)

[*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchClose*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

