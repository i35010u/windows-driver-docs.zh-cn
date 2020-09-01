---
title: 移植 DriverEntry
description: 移植 DriverEntry
ms.assetid: E880A45A-136C-480E-BE66-B61558F98227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b203bf98a7be98707b2c116b565f56d9e00c8bda
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191013"
---
# <a name="porting-driverentry"></a>移植 DriverEntry


在 WDM 和基于框架的驱动程序中， [**DriverEntry**](./driverentry-for-kmdf-drivers.md) 函数是主入口点。 这两个模型中的函数原型是相同的。 在 WDM 驱动程序中，当驱动程序首次加载到内存中时，系统会调用 **DriverEntry** 。 DriverEntry 在[**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)结构的**DriverExtension- &gt; AddDevice**字段中设置指向驱动程序的[*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的指针，并在驱动程序对象结构的**MajorFunction**数组中将指针设置为其 i/o 调度例程 \_ ，然后返回。 在基于框架的驱动程序中，系统会在加载驱动程序时调用框架的内部 **FxDriverEntry** 函数。 此内部函数初始化框架，然后调用驱动程序的 **DriverEntry** 函数。 **DriverEntry** 设置指向驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调的指针，并调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 来创建 WDFDRIVER 对象，如下面的示例所示：

```cpp
NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT  DriverObject
    IN PUNICODE_STRING RegistryPath
    )
{
    WDF_DRIVER_CONFIG config;

    WDF_DRIVER_CONFIG_INIT( &config,
                              ToasterEvtDeviceAdd );
    status = WdfDriverCreate(
                 DriverObject,
                 RegistryPath,
                 WDF_NO_OBJECT_ATTRIBUTES,
                 &config,
                 WDF_NO_HANDLE
             );

    return STATUS_SUCCESS;
}
```

**DriverEntry** 还初始化驱动程序所需的任何全局数据或资源，如创建后备链表列表或初始化跟踪。 请注意，虽然 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 返回 WDFDRIVER 对象的句柄，但驱动程序并不保留此句柄，这一点与 WDM 驱动程序可能不会保留 \_ 传递到其 **DriverEntry** 例程的驱动程序对象指针。 原因是相同的：只有几个驱动程序使用指向驱动程序对象的指针。

 

