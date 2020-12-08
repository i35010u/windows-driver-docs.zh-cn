---
title: WDF 驱动程序例程的 DriverEntry
description: DriverEntry 是加载驱动程序后调用的第一个驱动程序提供的例程。 它负责初始化驱动程序。
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
ms.openlocfilehash: ad81b90a9dec1745f5a53710e8639afd07577c48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814811"
---
# <a name="driverentry-for-wdf-drivers-routine"></a>WDF 驱动程序例程的 DriverEntry


\[适用于 KMDF 和 UMDF\]

**DriverEntry** 是加载驱动程序后调用的第一个驱动程序提供的例程。 它负责初始化驱动程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS DriverEntry(
  _In_ PDRIVER_OBJECT  DriverObject,
  _In_ PUNICODE_STRING RegistryPath
);
```

<a name="parameters"></a>参数
----------

*DriverObject* \[中\]  
指向 [**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 结构的指针，该结构表示驱动程序的 WDM 驱动程序对象。

*RegistryPath* \[中\]  
指向 [**UNICODE \_ 字符串**](/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string) 结构的指针，该字符串结构指定注册表中驱动程序的 [Parameters 项](./introduction-to-registry-keys-for-drivers.md) 的路径。

<a name="return-value"></a>返回值
------------

如果例程成功，则它必须返回状态 " \_ 成功"。 否则，它必须返回在 *ntstatus* 中定义的错误状态值之一。

<a name="remarks"></a>备注
-------

与所有 WDM 驱动程序一样，基于框架的驱动程序必须具有 **DriverEntry** 例程，该例程是在加载驱动程序后调用的。 基于框架的驱动程序的 **DriverEntry** 例程必须：

-   激活 [WPP 软件跟踪](./using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)。

    **DriverEntry** 应包含一个 [WPP \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏来激活软件跟踪。

-   调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)。

    对 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 的调用使驱动程序可以使用 Windows 驱动程序框架接口。  (在调用 **WdfDriverCreate** 之前，驱动程序无法调用其他框架例程 ) 

-   分配任何特定于设备的系统资源和可能需要的全局变量。

    通常，驱动程序将系统资源与单个设备相关联。 因此，基于框架的驱动程序在 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调中分配大多数资源，在检测到各个设备时将调用该回调。

    因为 UMDF 驱动程序的多个实例可能由单独的 Wudfhost 实例托管，所以全局变量可能无法在 UMDF 驱动程序的所有实例中使用。

-   从注册表获取驱动程序特定的参数。

    某些驱动程序从注册表中获取参数。 这些驱动程序可以调用 [**WdfDriverOpenParametersRegistryKey**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey) 来打开包含这些参数的注册表项。

-   提供 [DriverEntry 返回值](../kernel/driverentry-return-values.md)。

**注意**  UMDF 驱动程序在用户模式主机进程中运行，而 KMDF 驱动程序在系统进程的内核模式下运行。 此框架可能会将 UMDF 驱动程序的多个实例加载到主机进程的单独实例中。 因此：

 

-   如果在不同的主机进程中加载驱动程序的实例，则该框架可能会多次调用 UMDF 驱动程序的 DriverEntry 例程。 与此相反，框架只调用 KMDF 驱动程序的 DriverEntry 例程一次。
-   如果 UMDF 驱动程序在其 DriverEntry 例程中创建了一个全局变量，则该变量可能不可用于驱动程序的所有实例。 但是，KMDF 驱动程序在其 DriverEntry 例程中创建的全局变量可供驱动程序的所有实例使用。

有关何时调用基于框架的驱动程序的 **DriverEntry** 例程的详细信息，请参阅 [生成和加载 WDF 驱动程序](./building-and-loading-a-kmdf-driver.md)。

**DriverEntry** 例程未在 WDK 标头中声明。 静态驱动程序验证器 (SDV) 和其他验证工具可能需要如下所示的声明：

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

下面的代码示例演示了串行 (KMDF) 示例驱动程序的 **DriverEntry** 例程。

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
    SERIAL_FIRMWARE_DATA driverDefaults;

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


[**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)

[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)

