---
title: 移植 DriverEntry
description: 移植 DriverEntry
ms.assetid: E880A45A-136C-480E-BE66-B61558F98227
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dd941bc36d8d09cff1fd5b3c9a6d55001c787ad
ms.sourcegitcommit: ead145093395141164ec18a4764b19472ea9ff4b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65760600"
---
# <a name="porting-driverentry"></a>移植 DriverEntry


WDM 和基于框架的驱动程序中[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff540807)函数是主入口点。 函数原型是这两种模型中相同的。 在 WDM 驱动程序，系统将调用**DriverEntry**时驱动程序首次加载到内存。 DriverEntry 将指针设置为在驱动程序[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程中**DriverExtension-&gt;AddDevice**字段[ **驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)结构，在其 I/O 调度例程集指针**MajorFunction**驱动程序的数组\_对象结构，然后返回。 在基于框架的驱动程序，系统将调用框架的内部**FxDriverEntry**时加载驱动程序的函数。 此内部函数初始化框架，然后调用驱动程序的**DriverEntry**函数。 **DriverEntry**驱动程序的设置的指针[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调并调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)到创建 WDFDRIVER 对象，如以下示例所示：

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

**DriverEntry**还可以初始化该驱动程序要求，如创建后备链列表或初始化跟踪任何全局数据或资源。 请注意，虽然[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)返回的句柄 WDFDRIVER 对象，该驱动程序不会保留此句柄，就像 WDM 驱动程序可能不会保留该驱动程序\_对象指针，传递给其**DriverEntry**例程。 原因是相同的： 只有几个的驱动程序使用驱动程序对象的指针。

 

 





