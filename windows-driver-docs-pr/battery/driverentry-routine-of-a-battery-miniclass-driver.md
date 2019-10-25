---
title: 电池微型类驱动程序的 DriverEntry 例程
description: 电池微型类驱动程序的 DriverEntry 例程
ms.assetid: dc7c9f75-835b-4646-b30b-24c9dcb6ed2d
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- DriverEntry WDK 电池
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eda92cce32bb1e82e65d7b26a91ce297a690703
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832224"
---
# <a name="driverentry-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 DriverEntry 例程


## <span id="ddk_driverentry_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DRIVERENTRY_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程初始化 miniclass 驱动程序。

Miniclass 驱动程序的[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程设置以下特定于驱动程序的入口点：

-   *DriverObject*中的[*Unload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程&gt;**DriverUnload**-

-   *DriverObject*-中的驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程&gt;**DriverExtension**-&gt;**AddDevice**

-   *DriverObject*-中的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数&gt;**MajorFunction**\[[**IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)\]

-   *DriverObject*-中的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数&gt;**MajorFunction**\[[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)\]

-   *DriverObject*-中的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数&gt;**MajorFunction**\[[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)\]

-   *DriverObject*-中的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数&gt;**MajorFunction**\[[**IRP\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)\]

-   *DriverObject*-中的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数&gt;**MajorFunction**\[[**IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)\]

-   *DriverObject*-中的[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数&gt;**MAJORFUNCTION**\[[ **\_IRP\_SYSTEM\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)\]。

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

由于在 PnP 管理器调用 miniclass 驱动程序的*AddDevice*例程之前，特定于电池的状态信息是未知的，因此[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程不会初始化任何此类状态。 特定于设备的初始化是在*AddDevice*例程中执行的。

有关其他特定于例程的要求，请参阅以下主题：

[电池 Miniclass 驱动程序的 AddDevice 例程](adddevice-routine-of-a-battery-miniclass-driver.md)

[电池 Miniclass 驱动程序的 DispatchDeviceControl 例程](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[电池 Miniclass 驱动程序的 DispatchSystemControl 例程](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[卸载电池 Miniclass 驱动程序的例程](unload-routine-of-a-battery-miniclass-driver.md)

[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




