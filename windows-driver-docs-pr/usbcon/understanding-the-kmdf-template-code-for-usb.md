---
description: 了解基于 KMDF 的 USB 客户端驱动程序的源代码。
title: 'USB 客户端驱动程序代码结构 (KMDF) '
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 19373056298d44d706f3ab5b355623194e0f1a3c
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009889"
---
# <a name="understanding-the-usb-client-driver-code-structure-kmdf"></a>了解 USB 客户端驱动程序代码结构 (KMDF)


在本主题中，你将了解基于 aKMDF 的 USB 客户端驱动程序的源代码。 此代码示例由 Microsoft Visual Studio 2019 附带的 **USB 用户模式驱动程序**模板生成。

这些部分提供了有关模板代码的信息。

-   [驱动程序源代码](#driver-source-code)
-   [设备源代码](#device-source-code)
-   [队列源代码](#queue-source-code)
-   [相关主题](#related-topics)

有关生成 KMDF 模板代码的说明，请参阅 [如何编写第一个 USB 客户端驱动程序 (KMDF) ](tutorial--write-your-first-usb-client-driver--kmdf-.md)。

## <a name="driver-source-code"></a>驱动程序源代码


在 Windows 将驱动程序加载到内存中后， *driver 对象* 表示客户端驱动程序的实例。 驱动程序对象的完整源代码位于驱动程序 .h 和驱动程序中。

**驱动程序。h**

在讨论模板代码的详细信息之前，让我们来看一看标头文件中的一些声明 (与 KMDF 驱动程序开发相关的驱动程序 .h) 。

驱动程序包含这些文件，这些文件包含在 Windows 驱动程序工具包 (WDK) 中。

```ManagedCPlusPlus
#include <ntddk.h>
#include <wdf.h>
#include <usb.h>
#include <usbdlib.h>
#include <wdfusb.h>

#include "device.h"
#include "queue.h"
#include "trace.h"
```

对于 KMDF 驱动程序开发，始终包括 Ntddk 和 Wdf 标头文件。 标头文件包含编译 KMDF 驱动程序所需的方法和结构的各种声明和定义。

Usbdlib 和包括客户端驱动程序所需的用于 USB 设备的声明和定义。

Wdfusb 包括与框架提供的 USB i/o 目标对象进行通信所需的结构和方法的声明和定义。

WDK 中不包含设备 .h、Queue 和 node.js。 这些头文件由模板生成，并将在本主题的后面部分进行讨论。

Driver .h 中的下一个块提供 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程的函数角色类型声明，以及 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 和 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 事件回调例程。 所有这些例程均由驱动程序实现。 角色类型可帮助静态驱动程序验证器 (SDV) 分析驱动程序的源代码。 有关角色类型的详细信息，请参阅 [使用 KMDF 驱动程序的函数角色类型声明函数](../devtest/declaring-functions-by-using-function-role-types-for-kmdf-drivers.md)。

```ManagedCPlusPlus
DRIVER_INITIALIZE DriverEntry;
EVT_WDF_DRIVER_DEVICE_ADD MyUSBDriver_EvtDeviceAdd;
EVT_WDF_OBJECT_CONTEXT_CLEANUP MyUSBDriver_EvtDriverContextCleanup;
```

实现文件（Driver. c）包含以下代码块，这些代码使用 `alloc_text` 杂注来指定 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数和事件回调例程是否位于可分页内存中。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (INIT, DriverEntry)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDeviceAdd)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDriverContextCleanup)
#endif
```

请注意， [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 被标记为 INIT，而事件回调例程被标记为 PAGE。 INIT 部分表明， *DriverEntry* 的可执行代码是可分页的，驱动程序从其 *DriverEntry*返回后就会将其丢弃。 PAGE 部分指示代码不必始终保留在物理内存中;它在不使用时可以写入页面文件。 有关详细信息，请参阅 [锁定可分页的代码或数据](../kernel/locking-pageable-code-or-data.md)。

加载驱动程序后，Windows 将分配表示驱动程序的 [**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 结构。 然后，它调用驱动程序的入口点例程 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)，并传递指向结构的指针。 由于 Windows 按名称查找例程，因此每个驱动程序都必须实现一个名为 *DriverEntry*的例程。 例程执行驱动程序的初始化任务并指定驱动程序的事件回调例程到框架。

下面的代码示例显示模板生成的 DriverEntry 例程。

```ManagedCPlusPlus
NTSTATUS
DriverEntry(
    _In_ PDRIVER_OBJECT  DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    //
    // Initialize WPP Tracing
    //
    WPP_INIT_TRACING( DriverObject, RegistryPath );

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = MyUSBDriver_EvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
                           MyUSBDriver_EvtDeviceAdd
                           );

    status = WdfDriverCreate(DriverObject,
                             RegistryPath,
                             &attributes,
                             &config,
                             WDF_NO_HANDLE
                             );

    if (!NT_SUCCESS(status)) {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

[*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程有两个参数：指向由 Windows 分配的[**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)结构的指针，以及该驱动程序的注册表路径。 *RegistryPath*参数表示注册表中特定于驱动程序的路径。

在 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程中，驱动程序执行以下任务：

-   分配在驱动程序的生存期内必需的全局资源。 例如，在模板代码中，客户端驱动程序通过调用 [wpp \_ INIT \_ 跟踪](/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85)) 宏来分配 wpp 软件跟踪所需的资源。
-   向框架注册某些事件回调例程。

    若要注册事件回调，客户端驱动程序首先指定指向特定 WDF 结构中的 *EvtDriverXxx* 例程实现的指针。 然后，该驱动程序将调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 方法，并提供下一步) 中讨论 (的结构。

-   调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 方法，并检索 *框架驱动程序对象*的句柄。

    客户端驱动程序调用 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)后，框架会创建一个框架驱动程序对象，以表示客户端驱动程序。 当调用完成时，客户端驱动程序将接收 WDFDRIVER 句柄，并可以检索有关驱动程序的信息，如其注册表路径、版本信息等等 (参阅 [WDF Driver Object Reference](/windows-hardware/drivers/ddi/wdfdriver/)) 。

    请注意，framework 驱动程序对象不同于 [**driver \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)描述的 Windows 驱动程序对象。 同时，客户端驱动程序可以通过使用 WDFDRIVER 句柄并调用[**WdfGetDriver**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfgetdriver)方法来获取指向 Windows**驱动程序 \_ 对象**结构的指针。

[**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)调用后，框架伙伴与客户端驱动程序通信以与 Windows 进行通信。 框架充当 Windows 和驱动程序之间的抽象层，并处理大多数复杂的驱动程序任务。 客户端驱动程序向框架注册驱动程序感兴趣的事件。 发生某些事件时，Windows 会通知框架。 如果驱动程序为特定事件注册了事件回调，则框架将通过调用注册的事件回调通知驱动程序。 这样，就可以根据需要为驱动程序提供处理事件的机会。 如果驱动程序未注册其事件回调，则框架将继续对事件进行默认处理。

驱动程序必须注册的其中一个事件回调是 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。 框架准备好创建设备对象时，框架会调用驱动程序的 *EvtDriverDeviceAdd* 实现。 在 Windows 中，设备对象是用于加载客户端驱动程序的物理设备的函数的逻辑表示形式 (本主题后面的部分将) 。

驱动程序可以注册的其他事件回调为 [*EvtDriverUnload*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)、 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)和 [*EvtDestroyCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)。

在模板代码中，客户端驱动程序将注册以下两个事件： [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 和 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)。 驱动程序在[**wdf \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构中指定*EvtDriverDeviceAdd*实现的指针，并在[**wdf \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构中指定*EvtCleanupCallback*事件回调。

当 Windows 准备好释放 [**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 结构并卸载驱动程序时，框架会通过调用驱动程序的 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 实现将该事件报告给客户端驱动程序。 框架在删除框架驱动程序对象之前，将调用该回调。 客户端驱动程序可以释放它在 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)中分配的所有全局资源。 例如，在模板代码中，客户端驱动程序将停止在 *DriverEntry*中激活的 WPP 跟踪。

下面的代码示例演示客户端驱动程序的 EvtCleanupCallback 事件回调实现。

```ManagedCPlusPlus
VOID
MyUSBDriver_EvtDriverContextCleanup(
    _In_ WDFDRIVER Driver
    )
{
    UNREFERENCED_PARAMETER(Driver);

    PAGED_CODE ();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Stop WPP Tracing
    //
    WPP_CLEANUP( WdfDriverWdmGetDriverObject(Driver) );

}
```

USB 驱动程序堆栈识别设备后，总线驱动程序会为设备创建 (PDO) 的物理设备对象，并将 PDO 与设备节点相关联。 设备节点处于堆栈构造中，PDO 位于底部。 每个堆栈必须有一个 PDO，并 (筛选器 DOs) 具有筛选器设备对象，并可在其上方 (FDO) 函数设备对象。 有关详细信息，请参阅 [设备节点和设备堆栈](../debugger/device-node-and-stack-debugger-commands.md)。

下图显示了模板驱动程序 MyUSBDriver 的设备堆栈 \_ 。

![模板驱动程序的设备堆栈](images/usb-device-stack.png)

请注意名为 "我的 USB 设备" 的设备堆栈。 USB 驱动程序堆栈为设备堆栈创建 PDO。 在此示例中，PDO 与 Usbhub3.sys 相关联，这是 USB 驱动程序堆栈中包含的驱动程序之一。 作为设备的函数驱动程序，客户端驱动程序必须首先为设备创建 FDO，然后将其附加到设备堆栈的顶部。

对于基于 KMDF 的客户端驱动程序，框架将代表客户端驱动程序执行这些任务。 为了表示设备的 FDO，框架创建了 *框架设备对象*。 但是，客户端驱动程序可以指定框架用来配置新对象的某些初始化参数。 当框架调用驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 实现时，将向客户端驱动程序提供该机会。 创建对象并将 FDO 附加到设备堆栈顶部后，框架会向客户端驱动程序提供框架设备对象的 WDFDEVICE 句柄。 使用此句柄，客户端驱动程序可以执行各种与设备相关的操作。

下面的代码示例演示客户端驱动程序的 EvtDriverDeviceAdd 事件回调实现。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_EvtDeviceAdd(
    _In_    WDFDRIVER       Driver,
    _Inout_ PWDFDEVICE_INIT DeviceInit
    )
{
    NTSTATUS status;

    UNREFERENCED_PARAMETER(Driver);

    PAGED_CODE();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    status = MyUSBDriver_CreateDevice(DeviceInit);

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

在运行时， [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 的实现使用 [**分页 \_ 代码**](../kernel/mm-bad-pointer.md) 宏来检查是否正在适当的环境中为可分页代码调用例程。 请确保在声明所有变量后调用宏;否则，编译会失败，因为生成的源文件为 .c 文件而不是 .cpp 文件。

客户端驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 实现调用 MyUSBDriver \_ CreateDevice helper 函数来执行所需的任务。

下面的代码示例演示了 MyUSBDriver \_ CreateDevice helper 函数。 MyUSBDriver \_ CreateDevice 在中定义。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_CreateDevice(
    _Inout_ PWDFDEVICE_INIT DeviceInit
    )
{
    WDF_PNPPOWER_EVENT_CALLBACKS pnpPowerCallbacks;
    WDF_OBJECT_ATTRIBUTES   deviceAttributes;
    PDEVICE_CONTEXT deviceContext;
    WDFDEVICE device;
    NTSTATUS status;

    PAGED_CODE();

    WDF_PNPPOWER_EVENT_CALLBACKS_INIT(&pnpPowerCallbacks);
    pnpPowerCallbacks.EvtDevicePrepareHardware = MyUSBDriver_EvtDevicePrepareHardware;
    WdfDeviceInitSetPnpPowerEventCallbacks(DeviceInit, &pnpPowerCallbacks);

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&deviceAttributes, DEVICE_CONTEXT);

    status = WdfDeviceCreate(&DeviceInit, &deviceAttributes, &device);

    if (NT_SUCCESS(status)) {
        //
        // Get the device context and initialize it. WdfObjectGet_DEVICE_CONTEXT is an
        // inline function generated by WDF_DECLARE_CONTEXT_TYPE macro in the
        // device.h header file. This function will do the type checking and return
        // the device context. If you pass a wrong object  handle
        // it will return NULL and assert if run under framework verifier mode.
        //
        deviceContext = WdfObjectGet_DEVICE_CONTEXT(device);
        deviceContext->PrivateDeviceData = 0;

        //
        // Create a device interface so that applications can find and talk
        // to us.
        //
        status = WdfDeviceCreateDeviceInterface(
            device,
            &GUID_DEVINTERFACE_MyUSBDriver_,
            NULL // ReferenceString
            );

        if (NT_SUCCESS(status)) {
            //
            // Initialize the I/O Package and any Queues
            //
            status = MyUSBDriver_QueueInitialize(device);
        }
    }

    return status;
}
```

[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 有两个参数：在上一次调用 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)时创建的框架驱动程序对象的句柄，以及指向 [**WDFDEVICE \_ INIT**](../wdf/wdfdevice_init.md) 结构的指针。 框架分配 **WDFDEVICE \_ INIT** 结构并向其传递一个指针，以便客户端驱动程序可以使用要创建的框架设备对象的初始化参数填充结构。

在 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 实现中，客户端驱动程序必须执行以下任务：

-   调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 方法以检索新设备对象的 WDFDEVICE 句柄。

    [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)方法会使框架为 FDO 创建框架设备对象，并将其附加到设备堆栈的顶部。 在 **WdfDeviceCreate** 调用中，客户端驱动程序必须执行以下任务：

    -   [指定指向 \_ ](../wdf/wdfdevice_init.md)客户端驱动程序的即插即用 (PnP) power 回调函数中的客户端驱动程序的即插即用的指针。 首先在 [**WDF \_ PNPPOWER \_ 事件 \_ 回调**](/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_pnppower_event_callbacks) 结构中设置例程，并 \_ 通过调用 [**WdfDeviceInitSetPnpPowerEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) 方法与 WDFDEVICE INIT 关联。

        Windows 组件、PnP 和电源管理器会将与设备相关的请求发送给驱动程序，以响应 PnP 状态的更改 (例如 "已启动"、"已停止" 和 "已删除") 和电源状态 (如 "工作" 或 "挂起") 。 对于基于 KMDF 的驱动程序，框架会截获这些请求。 客户端驱动程序可以通过使用[**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)调用向框架注册名为*PnP 电源事件回调*的回调例程来接收有关请求的通知。 当 Windows 组件发送请求时，如果客户端驱动程序已注册，框架将处理这些请求并调用相应的 PnP 电源事件回调。

        客户端驱动程序必须实现的 PnP 电源事件回调例程之一是 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)。 当 PnP 管理器启动设备时，将调用该事件回调。 下一节将讨论 *EvtDevicePrepareHardware* 的实现。

    -   指定指向驱动程序的设备上下文结构的指针。 指针必须在 [**wdf \_ 对象 \_ 特性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构中设置，该结构是通过调用 [**wdf \_ 对象 \_ 特性 \_ INIT \_ 上下文 \_ 类型**](https://msdn.microsoft.com/library/windows/hardware/ff552400_init_context_type) 宏初始化的。

        设备上下文 (有时称为 "设备扩展") 是客户端驱动程序定义的数据结构 () 用于存储特定设备对象的信息。 客户端驱动程序将指向其设备上下文的指针传递到框架。 框架根据结构的大小分配内存块，并在框架设备对象中存储指向该内存位置的指针。 客户端驱动程序可以使用指针在设备上下文的成员中访问和存储信息。 有关设备上下文的详细信息，请参阅 [框架对象上下文空间](../wdf/framework-object-context-space.md)。

        [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)调用完成后，客户端驱动程序将接收新框架设备对象的句柄，该对象存储一个指向设备上下文框架所分配的内存块的指针。 现在，客户端驱动程序可以通过调用 **WdfObjectGet \_ 设备 \_ 上下文** 宏获取指向设备上下文的指针。

-   通过调用 [**WdfDeviceCreateDeviceInterface**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) 方法，为客户端驱动程序注册设备接口 GUID。 应用程序可以使用此 GUID 与驱动程序通信。 GUID 常量在标头（即公共 .h）中声明。
-   设置队列以实现到设备的 i/o 传输。 模板代码定义 MyUSBDriver \_ QueueInitialize，它是用于设置队列的帮助程序例程，在 [队列源代码](#queue-source-code) 部分中进行了讨论。

## <a name="device-source-code"></a>设备源代码


*设备对象*表示在内存中加载客户端驱动程序的设备的实例。 设备对象的完整源代码位于设备 .h 和设备 c 中。

**设备。h**

Device .h 头文件包含 common .h，后者包含项目中的所有文件使用的通用声明。

Device 中的下一个块声明客户端驱动程序的设备上下文。

```ManagedCPlusPlus
typedef struct _DEVICE_CONTEXT
{
    WDFUSBDEVICE UsbDevice;
    ULONG PrivateDeviceData;  // just a placeholder

} DEVICE_CONTEXT, *PDEVICE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(DEVICE_CONTEXT)
```

**设备 \_ 上下文**结构由客户端驱动程序定义，存储有关框架设备对象的信息。 它在 Device .h 中声明，并包含两个成员：框架的 USB 目标设备对象的句柄 (稍后讨论) 和占位符。 此结构将在后面的练习中展开。

Device .h 还包含 **WDF \_ DECLARE \_ 上下文 \_ TYPE** 宏，该宏将生成内联函数 **WdfObjectGet \_ 设备 \_ 上下文**。 客户端驱动程序可调用该函数，从框架设备对象检索指向内存块的指针。

以下代码行声明 MyUSBDriver \_ CreateDevice，这是一个帮助器函数，用于检索 USB 目标设备对象的 WDFUSBDEVICE 句柄。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_CreateDevice(
    _Inout_ PWDFDEVICE_INIT DeviceInit
    );
```

USBCreate 采用指向 [WDFDEVICE \_ INIT](../wdf/wdfdevice_init.md) 结构的指针作为其参数。 这是在调用客户端驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 实现时由框架传递的相同指针。 基本上，MyUSBDriver \_ CreateDevice 执行 *EvtDriverDeviceAdd*的任务。 上一部分讨论了 *EvtDriverDeviceAdd* 实现的源代码。

Device 中的下一行声明 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 事件回调例程的函数角色类型声明。 此事件回调由客户端驱动程序实现，并执行配置 USB 设备等任务。

```ManagedCPlusPlus
EVT_WDF_DEVICE_PREPARE_HARDWARE MyUSBDriver_EvtDevicePrepareHardware;
```

**设备 c**

设备 .c 实现文件包含以下代码块，这些代码使用 `alloc_text` 杂注来指定驱动程序的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 实现处于可分页内存中。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_CreateDevice)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDevicePrepareHardware)
#endif
```

在 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)的实现中，客户端驱动程序执行特定于 USB 的初始化任务。 这些任务包括注册客户端驱动程序、初始化 USB 特定的 i/o 目标对象以及选择 USB 配置。 下表显示了框架提供的专用 i/o 目标对象。 有关详细信息，请参阅 [USB I/o 目标](../wdf/usb-i-o-targets.md)。

| USB i/o 目标对象 (句柄)                    | 通过调用 ... 获取句柄。                                                          | 描述                                                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *USB 目标设备对象* (WDFUSBDEVICE )        | [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) | 表示一个 USB 设备，并提供用于检索设备描述符并将控制请求发送到设备的方法。                                                                                                                                                                                                                 |
| *USB 目标接口对象* (WDFUSBINTERFACE )  | [**WdfUsbTargetDeviceGetInterface**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)             | 表示单个接口，并提供客户端驱动程序可调用以选择备用设置和检索有关设置的信息的方法。                                                                                                                                                                              |
| *USB 目标管道对象* (WDFUSBPIPE)             | [**WdfUsbInterfaceGetConfiguredPipe**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)         | 表示终结点的单个管道，该终结点在接口的当前替代设置中进行配置。 USB 驱动程序堆栈选择所选配置中的每个接口，并设置接口中的每个终结点的通信通道。 在 USB 术语中，该通信通道称为 *管道*。 |

 

此代码示例演示了 EvtDevicePrepareHardware 的实现。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_EvtDevicePrepareHardware(
    _In_ WDFDEVICE Device,
    _In_ WDFCMRESLIST ResourceList,
    _In_ WDFCMRESLIST ResourceListTranslated
    )
{
    NTSTATUS status;
    PDEVICE_CONTEXT pDeviceContext;
    WDF_USB_DEVICE_CREATE_CONFIG createParams;
    WDF_USB_DEVICE_SELECT_CONFIG_PARAMS configParams;

    UNREFERENCED_PARAMETER(ResourceList);
    UNREFERENCED_PARAMETER(ResourceListTranslated);

    PAGED_CODE();

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    status = STATUS_SUCCESS;
    pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);

    if (pDeviceContext->UsbDevice == NULL) {

        //
        // Specifying a client contract version of 602 enables us to query for
        // and use the new capabilities of the USB driver stack for Windows 8.
        // It also implies that we conform to rules mentioned in the documentation
        // documentation for WdfUsbTargetDeviceCreateWithParameters.
        //
        WDF_USB_DEVICE_CREATE_CONFIG_INIT(&createParams,
                                         USBD_CLIENT_CONTRACT_VERSION_602
                                         );

        status = WdfUsbTargetDeviceCreateWithParameters(Device,
                                                    &createParams,
                                                    WDF_NO_OBJECT_ATTRIBUTES,
                                                    &pDeviceContext->UsbDevice
                                                    );

        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE,
                        "WdfUsbTargetDeviceCreateWithParameters failed 0x%x", status);
            return status;
        }

        //
        // Select the first configuration of the device, using the first alternate
        // setting of each interface
        //
        WDF_USB_DEVICE_SELECT_CONFIG_PARAMS_INIT_MULTIPLE_INTERFACES(&configParams,
                                                                     0,
                                                                     NULL
                                                                     );
        status = WdfUsbTargetDeviceSelectConfig(pDeviceContext->UsbDevice,
                                                WDF_NO_OBJECT_ATTRIBUTES,
                                                &configParams
                                                );

        if (!NT_SUCCESS(status)) {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE,
                        "WdfUsbTargetDeviceSelectConfig failed 0x%x", status);
            return status;
        }
    }

    TraceEvents(TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

下面更详细地介绍了模板代码实现的客户端驱动程序任务：

1.  指定客户端驱动程序的协定版本，准备向 Windows 加载的基础 USB 驱动程序堆栈注册自身。

    根据 USB 设备连接到的主机控制器，Windows 可以加载 USB 3.0 或 USB 2.0 驱动程序堆栈。 USB 3.0 驱动程序堆栈是 Windows 8 中的新增功能，并且支持 USB 3.0 规范定义的多个新功能，例如流功能。 新的驱动程序堆栈还实现了几项改进，如更好地跟踪和处理 USB 请求块 (URBs) ，可通过一组新的 URB 例程获得。 打算使用这些功能或调用新例程的客户端驱动程序必须指定 USBD \_ 客户端 \_ 合同 \_ 版本 \_ 602 合同版本。 USBD \_ 客户端 \_ 合同 \_ 版本 \_ 602 客户端驱动程序必须遵守一组特定规则。 有关这些规则的详细信息，请参阅 [最佳做法：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

    若要指定协定版本，客户端驱动程序必须通过调用[**wdf \_ usb \_ 设备 \_ create \_ config \_ INIT**](https://msdn.microsoft.com/library/windows/hardware/hh406503_init)宏来初始化一个 wdf usb 设备，并使用该协定版本[** \_ \_ \_ 创建 \_ 配置**](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_create_config)结构。

2.  调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) 方法。 此方法需要一个指向客户端驱动程序的框架设备对象的句柄，该对象是在驱动程序的[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)实现中调用[**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之前获取的。 **WdfUsbTargetDeviceCreateWithParameters**方法：
    -   将客户端驱动程序注册到基础 USB 驱动程序堆栈。
    -   检索由框架创建的 USB 目标设备对象的 WDFUSBDEVICE 句柄。 模板代码将句柄存储在设备上下文中的 USB 目标设备对象。 通过使用该句柄，客户端驱动程序可以获取有关设备的 USB 特定信息。

    **注意**   如果为，则必须调用[**WdfUsbTargetDeviceCreate**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate)而不是[**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/ff550077withconfig)
    -   你的客户端驱动程序不会调用 Windows 8 版 WDK 提供的新的 URB 例程集。

        如果客户端驱动程序调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)，则 USB 驱动程序堆栈假设通过调用 [**WdfUsbTargetDeviceCreateUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb) 或 [**WdfUsbTargetDeviceCreateIsochUrb**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)来分配所有 URBs。 这些方法分配的 URBs 具有不透明的 URB 上下文块，这些块由 USB 驱动程序堆栈用来加快处理速度。 如果客户端驱动程序使用的 URB 未由这些方法分配，则 USB 驱动程序会生成错误检查。

        有关 URB 分配的详细信息，请参阅 [分配和生成 URBs](how-to-add-xrb-support-for-client-drivers.md)。

    -   你的客户端驱动程序不打算遵循最佳做法中所述的一组规则 [：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

    此类驱动程序无需指定客户端协定版本，因此必须跳过步骤1。

     

3.  选择 USB 配置。

    在模板代码中，客户端驱动程序会选择 USB 设备中的 *默认配置* 。 默认配置包括设备的配置0和该配置内每个接口的备用设置0。

    若要选择默认配置，客户端驱动程序将 [**配置 \_ wdf \_ usb \_ \_ \_ 设备**](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_select_config_params) ，方法是调用 [**WDF \_ usb 设备， \_ \_ 选择 " \_ 配置 \_ 参数 \_ 初始化 \_ 多个 \_ 接口**](https://msdn.microsoft.com/library/windows/hardware/ff552600_init_multiple_interfaces) " 函数。 函数将 **类型** 成员初始化为 **WdfUsbTargetDeviceSelectConfigTypeMultiInterface** ，以指示如果有多个接口可用，则必须选择每个接口中的备用设置。 由于调用必须选择默认配置，因此客户端驱动程序在 *SettingPairs* 参数中指定 NULL，在 *NumberInterfaces* 参数中指定0。 完成后，WDF USB 设备的 **MultiInterface. NumberOfConfiguredInterfaces** 成员 ** \_ \_ \_ 选择 \_ 配置 \_ 参数** 表示选择了备用设置0的接口数。 不会修改其他成员。

    **注意**   如果客户端驱动程序要选择默认设置以外的其他设置，则驱动程序必须创建一个[**WDF \_ USB \_ 接口 \_ 设置 \_ 对**](/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_interface_setting_pair)结构的数组。 数组中的每个元素都指定设备定义的接口编号以及要选择的替代设置的索引。 该信息存储在设备的配置和接口描述符中，可以通过调用 [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor) 方法来获取这些信息。 然后，客户端驱动程序必须调用 [**WDF \_ usb \_ 设备 \_ 选择 \_ CONFIG \_ PARAMS \_ INIT \_ 多个 \_ 接口**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_device_select_config_params_init_multiple_interfaces) ，并将 **WDF \_ USB \_ 接口 \_ 设置 \_ 对** 数组传递到框架。

     

## <a name="queue-source-code"></a>队列源代码


*Framework queue 对象*表示特定框架设备对象的 i/o 队列。 队列对象的完整源代码位于 Queue 和 Queue 中。

**Queue。h**

为框架的队列对象引发的事件声明事件回调例程。

Queue 中的第一个块声明队列上下文。

```ManagedCPlusPlus
typedef struct _QUEUE_CONTEXT {

    ULONG PrivateDeviceData;  // just a placeholder

} QUEUE_CONTEXT, *PQUEUE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(QUEUE_CONTEXT, QueueGetContext)
```

与设备上下文类似，队列上下文是由客户端定义的数据结构，用于存储有关特定队列的信息。

下一行代码声明 MyUSBDriver \_ QueueInitialize 函数，该函数创建并初始化框架队列对象。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_QueueInitialize(
    _In_ WDFDEVICE Device
    );
```

下面的代码示例声明了 [*EvtIoDeviceControl*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control) 事件回调例程的函数角色类型声明。 事件回调由客户端驱动程序实现，并且在框架处理设备 i/o 控制请求时进行调用。

```ManagedCPlusPlus
EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL MyUSBDriver_EvtIoDeviceControl;
```

**Queue**

实现文件（即 Queue）包含以下代码块，该代码块使用 `alloc_text` 杂注来指定驱动程序的 MyUSBDriver QueueInitialize 的实现 \_ 是可分页内存。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_QueueInitialize)
#endif
```

WDF 提供框架队列对象来处理客户端驱动程序的请求流。 当客户端驱动程序调用 [**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) 方法时，框架会创建框架队列对象。 在该调用中，客户端驱动程序可以在框架创建队列之前指定某些配置选项。 这些选项包括：队列是否处于电源管理状态、是否允许长度为零的请求，或者是否为驱动程序的默认队列。 单个框架队列对象可以处理多种类型的请求，如读取、写入和设备 i/o 控制。 客户端驱动程序可以指定每个请求的事件回调。

客户端驱动程序还必须指定派单类型。 队列对象的调度类型决定了框架如何向客户端驱动程序发送请求。 传递机制可以是连续的，也可以是由客户端驱动程序定义的自定义机制。 对于顺序队列，在客户端驱动程序完成以前的请求之前，不会传递请求。 在并行调度模式下，框架会在请求到达 i/o 管理器后立即转发请求。 这意味着客户端驱动程序可以在处理另一个请求时接收一个请求。 在自定义机制中，当驱动程序准备好处理下一个请求时，客户端会手动从框架队列对象中提取下一个请求。

通常，客户端驱动程序必须在驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 事件回调中设置队列。 模板代码提供了 helper 例程 MyUSBDriver \_ QueueInitialize，用于初始化框架队列对象。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_QueueInitialize(
    _In_ WDFDEVICE Device
    )
{
    WDFQUEUE queue;
    NTSTATUS status;
    WDF_IO_QUEUE_CONFIG    queueConfig;

    PAGED_CODE();
    
    //
    // Configure a default queue so that requests that are not
    // configure-fowarded using WdfDeviceConfigureRequestDispatching to goto
    // other queues get dispatched here.
    //
    WDF_IO_QUEUE_CONFIG_INIT_DEFAULT_QUEUE(
         &queueConfig,
        WdfIoQueueDispatchParallel
        );

    queueConfig.EvtIoDeviceControl = MyUSBDriver_EvtIoDeviceControl;

    status = WdfIoQueueCreate(
                 Device,
                 &queueConfig,
                 WDF_NO_OBJECT_ATTRIBUTES,
                 &queue
                 );

    if( !NT_SUCCESS(status) ) {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_QUEUE, "WdfIoQueueCreate failed %!STATUS!", status);
        return status;
    }

    return status;
}
```

若要设置队列，客户端驱动程序将执行以下任务：

1.  在 [**WDF \_ IO \_ 队列 \_ 配置**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config) 结构中指定队列的配置选项。 模板代码使用 [**WDF \_ IO \_ QUEUE \_ CONFIG \_ INIT \_ 默认 \_ 队列**](https://msdn.microsoft.com/library/windows/hardware/ff552359_init_default_queue) 函数初始化结构。 函数将 queue 对象指定为默认队列对象，并进行电源管理，并并行接收请求。
2.  为队列的 i/o 请求添加客户端驱动程序的事件回调。 在模板中，客户端驱动程序为设备 i/o 控制请求指定一个指向其事件回调的指针。
3.  调用 [**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) ，以检索由框架创建的框架队列对象的 WDFQUEUE 句柄。

下面是队列机制的工作方式。 若要与 USB 设备通信，应用程序首先通过调用 **SetDixxx** 例程和 [**CreateHandle**](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)打开设备的句柄。 使用此句柄，应用程序将使用特定控制代码调用 [**DeviceIoControl**](/previous-versions/windows/desktop/api/deviceaccess/nn-deviceaccess-ideviceiocontrol) 函数。 根据控制代码的类型，应用程序可以在该调用中指定输入和输出缓冲区。 调用最终由 i/o 管理器接收，该管理器会创建一个 (IRP) 请求，并将其转发到客户端驱动程序。 框架截获请求，创建框架请求对象，并将其添加到框架队列对象。 在这种情况下，由于客户端驱动程序为设备 i/o 控制请求注册了其事件回调，因此框架会调用回调。 另外，由于队列对象是用 WdfIoQueueDispatchParallel 标志创建的，因此，一旦向队列中添加了该请求，就会调用该回调。

```ManagedCPlusPlus
VOID
MyUSBDriver_EvtIoDeviceControl(
    _In_ WDFQUEUE Queue,
    _In_ WDFREQUEST Request,
    _In_ size_t OutputBufferLength,
    _In_ size_t InputBufferLength,
    _In_ ULONG IoControlCode
    )
{
    TraceEvents(TRACE_LEVEL_INFORMATION, 
                TRACE_QUEUE, 
                "!FUNC! Queue 0x%p, Request 0x%p OutputBufferLength %d InputBufferLength %d IoControlCode %d", 
                Queue, Request, (int) OutputBufferLength, (int) InputBufferLength, IoControlCode);

    WdfRequestComplete(Request, STATUS_SUCCESS);

    return;
}
```

当框架调用客户端驱动程序的事件回调时，它会将句柄传递给包含请求 (的框架请求对象及其输入和输出缓冲区) 应用程序发送。 此外，它还向包含请求的框架队列对象发送句柄。 在事件回调中，客户端驱动程序会根据需要处理请求。 模板代码只完成请求。 客户端驱动程序可以执行更多涉及的任务。 例如，如果应用程序请求某些设备信息，则在事件回调中，客户端驱动程序可以创建 USB 控制请求并将其发送到 USB 驱动程序堆栈以检索请求的设备信息。 Usb 控件 [传输](usb-control-transfer.md)中讨论了 usb 控制请求。

## <a name="related-topics"></a>相关主题
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  
[WinUSB](winusb.md)  
[将第一个 USB 客户端驱动程序写入 (UMDF) ](implement-driver-entry-for-a-usb-driver--umdf-.md)  
[ (KMDF 中写入第一个 USB 客户端驱动程序) ](tutorial--write-your-first-usb-client-driver--kmdf-.md)