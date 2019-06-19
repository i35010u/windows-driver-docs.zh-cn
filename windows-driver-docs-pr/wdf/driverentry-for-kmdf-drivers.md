---
title: WDF 驱动程序例程的 DriverEntry
description: DriverEntry 是加载驱动程序后，将调用的第一个驱动程序提供例程。 它负责初始化驱动程序。
ms.assetid: b49d1767-7cfd-45bb-a2be-0597f7373e79
keywords:
- DriverEntry 例程
- 例程
- DRIVER_INITIALIZE 例程
topic_type:
- apiref
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 57c4979c6e7c9d2354b040346adcdc0d665404e8
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161536"
---
# <a name="driverentry-for-wdf-drivers-routine"></a>WDF 驱动程序例程的 DriverEntry


\[适用于 KMDF 和 UMDF\]

**DriverEntry**的驱动程序加载后，将调用的第一个驱动程序提供例程。 它负责初始化驱动程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>Parameters
----------

*DriverObject* \[in\]  
一个指向[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)结构，它表示驱动程序的 WDM 驱动程序对象。

*RegistryPath* \[in\]  
一个指向[ **UNICODE\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff564879)结构，它指定的驱动程序的路径[Parameters 项](https://msdn.microsoft.com/library/windows/hardware/ff544262)注册表中。

<a name="return-value"></a>返回值
------------

如果该例程成功，它必须返回状态\_成功。 否则，它必须返回中定义的错误状态值之一*ntstatus.h*。

<a name="remarks"></a>备注
-------

基于框架的驱动程序必须具有所有 WDM 驱动程序，如**DriverEntry**例程，驱动程序加载后，将调用。 基于框架的驾驶**DriverEntry**例程必须：

-   激活[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/dn940485)。

    **DriverEntry**应包括[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)宏以激活软件跟踪。

-   调用[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)。

    在调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175) ，驱动程序以使用 Windows 驱动程序框架接口。 (该驱动程序不能调用之前调用其他 framework 例程**WdfDriverCreate**。)

-   分配的任何非特定于设备的系统资源和可能需要的全局变量。

    通常情况下，驱动程序将与单个设备关联的系统资源。 因此，基于框架的驱动程序分配中的大多数资源[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调，它在检测到各个设备时调用。

    UMDF 驱动程序的多个实例可能由 Wudfhost 的单独实例托管，因为全局变量可能不能跨 UMDF 驱动程序的所有实例。

-   从注册表获取特定于驱动程序的参数。

    某些驱动程序从注册表获取参数。 这些驱动程序可以调用[ **WdfDriverOpenParametersRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547202)以打开包含这些参数的注册表项。

-   提供[DriverEntry 返回值](https://msdn.microsoft.com/library/windows/hardware/ff544119)。

**请注意**  UMDF 驱动程序在用户模式下主机进程中，运行的同时 KMDF 驱动程序在系统进程中的内核模式下运行。 该框架可能会加载到主机进程的单独实例 UMDF 驱动程序的多个实例。 结果：

 

-   该框架可能 UMDF 驱动程序的 DriverEntry 例程多次调用如果加载不同的宿主进程中的驱动程序的实例。 与此相反，框架在仅一次调用 KMDF 驱动程序的 DriverEntry 例程。
-   如果 UMDF 驱动程序时在其 DriverEntry 例程创建的全局变量，变量可能可能不可用的驱动程序的所有实例。 但是，KMDF 驱动程序创建其 DriverEntry 例程中的全局变量可供该驱动程序的所有实例。

有关何时的详细信息基于框架的驾驶**DriverEntry**调用例程，请参阅[构建和 WDF 驱动程序加载](https://msdn.microsoft.com/library/windows/hardware/ff540730)。

**DriverEntry**例程不在 WDK 标头中声明。 Static Driver Verifier (SDV) 和其他验证工具可能需要的声明如下所示：

``` syntax
DRIVER_INITIALIZE MyDriverEntry;

NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT  DriverObject,
    IN PUNICODE_STRING  RegistryPath
    )
{
// Function body
}
```

<a name="examples"></a>示例
--------

下面的代码示例显示了串行 (KMDF) 示例驱动程序**DriverEntry**例程。

```cpp
NTSTATUS
DriverEntry(
    IN PDRIVER_OBJECT  DriverObject,
    IN PUNICODE_STRING  RegistryPath
    )
{
    WDF_DRIVER_CONFIG  config;
    WDFDRIVER  hDriver;
    NTSTATUS  status;
    WDF_OBJECT_ATTRIBUTES  attributes;

    //
    // Initialize WPP tracing.
    //
    WPP_INIT_TRACING(
                     DriverObject,
                     RegistryPath
                     );

    SerialDbgPrintEx(
                     TRACE_LEVEL_INFORMATION,
                     DBG_INIT,
                     "Serial Sample (WDF Version) - Built %s %s\n",
                     __DATE__, __TIME__
                     );
    //
    // Register a cleanup callback function (which calls WPP_CLEANUP)
    // for the framework driver object. The framework will call
    // the cleanup callback function when it deletes the driver object,
    // before the driver is unloaded.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = SerialEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(
                           &config,
                           SerialEvtDeviceAdd
                           );

    status = WdfDriverCreate(
                             DriverObject,
                             RegistryPath,
                             &attributes,
                             &config,
                             &hDriver
                             );
    if (!NT_SUCCESS(status)) {
        SerialDbgPrintEx(
                         TRACE_LEVEL_ERROR,
                         DBG_INIT,
                         "WdfDriverCreate failed with status 0x%x\n",
                         status
                         );
        //
        // Clean up tracing here because WdfDriverCreate failed.
        //
        WPP_CLEANUP(DriverObject);
        return status;
    }

    //
    // Call an internal routine to obtain registry values
    // to use for all the devices that the driver 
    // controls, including whether or not to break on entry.
    //
    SerialGetConfigDefaults(
                            &driverDefaults,
                            hDriver
                            );

    //
    // Break on entry if requested bt registry value.
    //
    if (driverDefaults.ShouldBreakOnEntry) {
        DbgBreakPoint();
    }

    return status;
}
```

## <a name="see-also"></a>请参阅


[**WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)

[*EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)

 

 






