---
Description: 了解有关客户端的基于 KMDF 的 USB 驱动程序的源代码。
title: USB 客户端驱动程序代码结构 (KMDF)
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: bd70173383d613def89ed10567e892846485e5ce
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815116"
---
# <a name="understanding-the-usb-client-driver-code-structure-kmdf"></a>了解 USB 客户端驱动程序代码结构 (KMDF)


在本主题中，您将学习如何 aKMDF 基于 USB 客户端驱动程序的源代码。 由生成的代码示例**USB 用户模式驱动程序**Microsoft Visual Studio 2019 中包含的模板。

以下各节提供有关模板代码的信息。

-   [驱动程序源代码](#driver-source-code)
-   [设备的源代码](#device-source-code)
-   [队列的源代码](#queue-source-code)
-   [相关的主题](#related-topics)

有关生成 KMDF 模板代码的说明，请参阅[如何编写第一个 USB 客户端驱动程序 (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)。

## <a name="driver-source-code"></a>驱动程序源代码


*驱动程序对象*后 Windows 加载该驱动程序在内存中的表示客户端驱动程序的实例。 在 Driver.h 和 Driver.c 是驱动程序对象的完整源代码。

**Driver.h**

在讨论之前的模板代码的详细信息，让我们看看标头文件 (Driver.h) KMDF 驱动程序开发相关的一些声明。

Driver.h，包含这些文件，包括 Windows Driver Kit (WDK) 中。

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

Ntddk.h 和 Wdf.h 标头文件都始终包含 KMDF 驱动程序开发。 标头文件包括各种声明和定义的方法和需要编译 KMDF 驱动程序的结构。

Usb.h 和 Usbdlib.h 包括声明和定义的结构和所需的 USB 设备的客户端驱动程序的例程。

Wdfusb.h 包括声明和定义的结构和与框架提供的 USB I/O 目标对象进行通信所需的方法。

WDK 中不包括 Device.h、 Queue.h、 和 Trace.h。 这些标头文件由模板生成和本主题后面所述。

下一步中 Driver.h 块提供函数的角色类型声明[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，并[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)并[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)事件回调例程。 驱动程序实现了所有这些例程。 角色类型可帮助 Static Driver Verifier (SDV) 分析驱动程序的源代码。 有关角色类型的详细信息，请参阅[KMDF 驱动程序中使用函数角色类型声明函数](https://msdn.microsoft.com/library/windows/hardware/ff544643)。

```ManagedCPlusPlus
DRIVER_INITIALIZE DriverEntry;
EVT_WDF_DRIVER_DEVICE_ADD MyUSBDriver_EvtDeviceAdd;
EVT_WDF_OBJECT_CONTEXT_CLEANUP MyUSBDriver_EvtDriverContextCleanup;
```

实现文件中，Driver.c，包含以下使用的代码块`alloc_text`杂注指定是否[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数和事件的回调例程位于可分页内存。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (INIT, DriverEntry)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDeviceAdd)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDriverContextCleanup)
#endif
```

请注意， [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)被标记为 INIT，而事件回调例程标记为页。 INIT 部分指示的可执行代码*DriverEntry*是可分页，丢弃该驱动程序返回从其*DriverEntry*。 页部分指示代码不需要保留在物理内存的时间;它可以不使用时写入到页面文件中。 有关详细信息，请参阅[锁定可分页代码或数据](https://msdn.microsoft.com/library/windows/hardware/ff554307)。

稍后加载您的驱动程序后，Windows 将分配[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)结构，它表示您的驱动程序。 然后，它调用您的驱动程序的入口点例程[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)，并将指针传递给结构。 由于 Windows 按名称查找该例程，每个驱动程序必须实现名为的例程*DriverEntry*。 例程执行驱动程序的初始化任务，并指定框架的驱动程序的事件回调例程。

下面的代码示例显示了由模板生成的 DriverEntry 例程。

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

[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程具有两个参数： 指向的指针[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)分配的结构通过 Windows，并驱动程序的注册表路径。 *RegistryPath*参数表示在注册表中的特定于驱动程序的路径。

在中[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，该驱动程序执行以下任务：

-   分配所需的驱动程序的生存期内的全局资源。 例如，在模板代码中，客户端驱动程序分配资源所需的 WPP 软件跟踪通过调用[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)宏。
-   向框架注册某些事件回调例程。

    若要注册事件回调，客户端驱动程序，首先指定到其实现的指针*EvtDriverXxx*某些 WDF 结构中的例程。 然后，该驱动程序调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)方法并提供这些结构 （下一步中所述）。

-   调用[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)方法，并检索的句柄*framework 驱动程序对象*。

    客户端驱动程序调用后[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)，框架将创建一个框架驱动程序对象来表示客户端驱动程序。 调用完成时，客户端驱动程序接收 WDFDRIVER 句柄，并可以检索有关该驱动程序，如注册表路径、 版本信息等的信息 (请参阅[WDF 驱动程序对象引用](https://msdn.microsoft.com/library/windows/hardware/dn265636))。

    请注意，所描述的 Windows 驱动程序对象从不同的 framework 驱动程序对象[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)。 在任何时候，客户端驱动程序可以获得一个指向 Windows**驱动程序\_对象**结构的使用 WDFDRIVER 句柄并调用[ **WdfGetDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff547336)方法。

之后[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)调用，使用客户端驱动程序框架合作伙伴，能够与 Windows 通信。 框架可用作 Windows 和驱动程序之间的抽象层，并处理的大多数复杂的驱动程序任务。 客户端驱动程序向框架注册为事件该驱动程序感兴趣。 发生某些事件时，Windows 会通知框架。 如果驱动程序已注册的特定事件的事件回调，框架会通过调用已注册的事件回调通知驱动程序。 通过此操作，该驱动程序都有机会以处理事件，如果需要。 如果该驱动程序未注册其事件回调，该框架将继续进行默认处理的事件。

该驱动程序必须注册事件回调之一是[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)。 框架调用的驱动程序*EvtDriverDeviceAdd*实现时 framework 是否准备好创建设备对象。 在 Windows 中，一个设备对象是函数的为其加载客户端驱动程序 （在本主题后面讨论） 的物理设备的逻辑表示形式。

该驱动程序可以注册其他事件回调[ *EvtDriverUnload*](https://msdn.microsoft.com/library/windows/hardware/ff541694)， [ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)，和[*EvtDestroyCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540841)。

在模板代码中，客户端驱动程序将注册两个事件：[*EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)并[ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)。 该驱动程序指定一个指向其实现*EvtDriverDeviceAdd*中[ **WDF\_驱动程序\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551300)结构和*EvtCleanupCallback*中的事件回调[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构。

当 Windows 是已准备好发布[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)结构和卸载该驱动程序，框架会通过调用驱动程序的客户端驱动程序报告该事件[*EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)实现。 它将删除 framework 驱动程序对象之前，框架将调用该回调。 客户端驱动程序可以释放它分配了中的所有全局资源及其[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)。 例如，在模板代码中，客户端驱动程序将停止在已激活的 WPP 跟踪*DriverEntry*。

下面的代码示例显示了客户端驱动程序的 EvtCleanupCallback 事件回调实现。

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

该设备识别通过 USB 驱动程序堆栈后，总线驱动程序创建设备的物理设备对象 (PDO)，并将 PDO 与设备节点相关联。 设备节点是堆栈信息，其中 PDO 是在底部。 每个堆栈必须具有一个 PDO，并且可以具有筛选器 （筛选 DOs） 的设备对象和其上的一个函数设备对象 (FDO)。 有关详细信息，请参阅[设备节点和设备堆栈](https://msdn.microsoft.com/library/windows/hardware/hh406296)。

此图显示了模板驱动程序，MyUSBDriver 设备堆栈\_.sys。

![模板驱动程序的设备堆栈](images/usb-device-stack.png)

请注意，堆栈名为"My USB 设备"的设备。 USB 驱动程序堆栈创建设备堆栈 PDO。 在示例中，PDO 是与 Usbhub3.sys，这是一个 USB 驱动程序堆栈中包含的驱动程序相关联。 作为设备的函数驱动程序，客户端驱动程序必须先创建设备 FDO，然后将其附加到设备堆栈的顶部。

对于 KMDF 基于客户端驱动程序，框架执行这些任务代表客户端驱动程序。 若要表示为设备 FDO，则框架将创建*framework 设备对象*。 客户端驱动程序但是，可以指定某些框架将使用配置新的对象的初始化参数。 框架调用的驱动程序时，为客户端驱动程序指定机会[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)实现。 创建对象并 FDO 附加到设备堆栈的顶部后，该框架提供的 WDFDEVICE 句柄的 framework 设备对象的客户端驱动程序。 通过使用此句柄，客户端驱动程序可以执行各种与设备相关的操作。

下面的代码示例显示了客户端驱动程序的 EvtDriverDeviceAdd 事件回调实现。

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

在运行时，实现[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)使用[ **PAGED\_代码**](https://msdn.microsoft.com/library/windows/hardware/ff558773)宏，以检查适用于可分页的代码的环境中调用例程。 请确保声明所有变量; 之后调用该宏否则，编译失败，因为生成的源代码文件是.c 文件而不是.cpp 文件。

客户端驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)实现调用 MyUSBDriver\_CreateDevice 帮助器函数来执行所需的任务。

下面的代码示例显示了 MyUSBDriver\_CreateDevice 帮助器函数。 MyUSBDriver\_CreateDevice Device.c 中定义。

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

[*EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)有两个参数： framework 驱动程序对象的句柄到上一个调用中创建[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)，以及指向[**WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。 Framework 分配**WDFDEVICE\_INIT**结构，并将其传递一个指针，以便客户端驱动程序可以填充的结构与要创建的框架设备对象的初始化参数。

在中[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)实现中，客户端驱动程序必须执行以下任务：

-   调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)方法来检索 WDFDEVICE 句柄的新的设备对象。

    [ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)方法会导致框架为 FDO 创建 framework 设备对象并将其附加到设备堆栈的顶部。 在中**WdfDeviceCreate**调用，客户端驱动程序必须执行以下任务：

    -   在指定框架指定到客户端驱动程序的插即用 (PnP) power 回调例程的指针[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。 例程首先集中[ **WDF\_PNPPOWER\_事件\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff552416)结构并且与 WDFDEVICE 然后关联\_通过调用 INIT[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135)方法。

        Windows 组件 PnP 和电源管理器、 将与设备相关的请求发送到响应即插即用的状态 （如启动，停止和删除） 中的更改中的驱动程序和电源状态 （如处理或挂起）。 对于基于 KMDF 驱动程序，该框架截获这些请求。 通过注册调用的回调例程，可以获取客户端驱动程序通知有关请求*PnP 电源事件的回调*使用框架，通过使用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)调用。 当 Windows 组件发送请求时，框架处理它们，并调用相应的即插即用电源事件回调，如果客户端驱动程序已注册。

        客户端驱动程序必须实现的即插即用电源事件回调例程之一是[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)。 PnP 管理器启动设备时，会调用该事件回调。 为实现*EvtDevicePrepareHardware*下一节中讨论。

    -   指定指向驱动程序的设备上下文结构的指针。 必须在设置指针[ **WDF\_对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构，它通过调用来初始化[ **WDF\_对象\_特性\_INIT\_上下文\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff552400_init_context_type)宏。

        设备上下文 （有时称为设备扩展） 是用于存储有关特定的设备对象的信息 （由客户端驱动程序定义） 的数据结构。 客户端驱动程序将指针传递到框架及其设备上下文。 框架中分配的基础结构的大小的内存块，并在 framework 设备对象中存储指向该内存位置的指针。 客户端驱动程序可以使用指针来访问和信息存储在设备上下文的成员。 关于设备上下文的详细信息，请参阅[框架对象上下文空间](https://msdn.microsoft.com/library/windows/hardware/ff542873)。

        之后[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)调用完成后，客户端驱动程序将收到新的 framework 设备对象，它存储设备的框架所分配的内存块的指针的句柄上下文。 客户端驱动程序可以立即获得一个指向设备上下文通过调用**WdfObjectGet\_设备\_上下文**宏。

-   通过调用注册的客户端驱动程序的设备接口的 GUID [ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)方法。 应用程序能够通过使用此 GUID 与驱动程序。 在标题中，声明的 GUID 常量 public.h。
-   设置到设备的 I/O 传输队列。 模板代码定义 MyUSBDriver\_QueueInitialize，设置队列，其中讨论了一个帮助器例程[排队源代码](#queue-source-code)部分。

## <a name="device-source-code"></a>设备的源代码


*设备对象*表示为其客户端驱动程序加载到内存中的设备的实例。 设备对象的完整源代码是 Device.h 和 Device.c 中。

**Device.h**

Device.h 标头文件包括 public.h，其中包含由项目中的所有文件的常用声明。

下一个块 Device.h 中的声明的客户端驱动程序的设备上下文。

```ManagedCPlusPlus
typedef struct _DEVICE_CONTEXT
{
    WDFUSBDEVICE UsbDevice;
    ULONG PrivateDeviceData;  // just a placeholder

} DEVICE_CONTEXT, *PDEVICE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE(DEVICE_CONTEXT)
```

**设备\_上下文**结构定义的客户端驱动程序，并将存储有关 framework 设备对象的信息。 它在 Device.h 中声明，包含两个成员： 的句柄框架的 USB 目标设备对象 （稍后讨论） 和一个占位符。 在更高版本的练习中，将扩展此结构。

此外包括 Device.h **WDF\_DECLARE\_上下文\_类型**宏，生成的内联函数， **WdfObjectGet\_设备\_上下文**。 客户端驱动程序可以调用该函数可检索 framework 设备对象指针的内存块。

以下代码行声明 MyUSBDriver\_CreateDevice，检索的 WDFUSBDEVICE 句柄的 USB 目标设备对象的帮助器函数。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_CreateDevice(
    _Inout_ PWDFDEVICE_INIT DeviceInit
    );
```

USBCreate 采用一个指向[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构作为其参数。 这是相同的指针调用客户端驱动程序时由框架传递[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)实现。 基本上，MyUSBDriver\_CreateDevice 执行的任务*EvtDriverDeviceAdd*。 源代码*EvtDriverDeviceAdd*上一节中讨论实现。

Device.h 中的下一行声明的函数角色类型声明[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)事件回调例程。 事件回调由客户端驱动程序实现，并执行任务，例如配置 USB 设备。

```ManagedCPlusPlus
EVT_WDF_DEVICE_PREPARE_HARDWARE MyUSBDriver_EvtDevicePrepareHardware;
```

**Device.c**

Device.c 实现文件包含以下使用的代码块`alloc_text`杂注指定的驱动程序的实现[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)中可分页内存。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_CreateDevice)
#pragma alloc_text (PAGE, MyUSBDriver_EvtDevicePrepareHardware)
#endif
```

中的实现[ *EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)，客户端驱动程序执行特定于 USB 的初始化任务。 这些任务包括注册客户端驱动程序、 初始化特定于 USB 的 I/O 目标对象，以及选择 USB 配置。 下表显示了由框架提供的专用的 I/O 目标对象。 有关详细信息，请参阅[USB I/O 目标](https://msdn.microsoft.com/library/windows/hardware/ff544752)。

| USB I/O 目标对象 （句柄）                   | 通过调用获取的句柄...                                                          | 描述                                                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *USB 目标设备对象*(WDFUSBDEVICE)       | [**WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428) | 表示 USB 设备，并提供用于检索设备描述符并将控制请求发送到设备的方法。                                                                                                                                                                                                                 |
| *USB 目标接口对象*(WDFUSBINTERFACE) | [**WdfUsbTargetDeviceGetInterface**](https://msdn.microsoft.com/library/windows/hardware/ff550092)             | 表示单个接口，并提供客户端驱动程序可以调用来选择备用设置和检索有关设置的信息的方法。                                                                                                                                                                              |
| *USB 目标管道对象*(WDFUSBPIPE)            | [**WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)         | 表示单个管道接口的当前备用设置中配置的终结点。 USB 驱动程序堆栈中所选的配置选择每个接口，并设置在界面中每个终结点的通信通道。 在 USB 术语中，该通信通道被称为*管道*。 |

 

此代码示例演示 EvtDevicePrepareHardware 的实现。

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

下面是深入研究，客户端驱动程序的任务，由模板代码实现：

1.  指定在准备将自身注册为基础的 USB 驱动程序堆栈，加载的 Windows 客户端驱动程序的协定版本。

    Windows 可以加载 USB 3.0 或 USB 2.0 驱动程序堆栈，具体取决于 USB 设备连接到主控制器。 USB 3.0 驱动程序堆栈是 Windows 8 中的新增功能，支持 USB 3.0 规范，如流功能所定义的多项新功能。 新的驱动程序堆栈还实现了多项改进，例如更好地跟踪和处理的 USB 请求块 (URBs)，可通过一组新的 URB 例程。 想要使用这些功能或调用新的例程的客户端驱动程序必须指定 USBD\_客户端\_协定\_版本\_602 协定版本。 USBD\_客户端\_协定\_版本\_602 客户端驱动程序必须遵守特定的规则集。 有关这些规则的详细信息，请参阅[最佳实践：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

    若要指定的协定版本，客户端驱动程序必须初始化[ **WDF\_USB\_设备\_创建\_配置**](https://msdn.microsoft.com/library/windows/hardware/hh406503)结构通过调用协定版本[ **WDF\_USB\_设备\_创建\_配置\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/hh406503_init)宏。

2.  调用[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)方法。 该方法要求客户端驱动程序通过调用前面获取的 framework 设备对象的句柄[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)中的驱动程序的实现[ *EvtDriverDeviceAdd*](https://msdn.microsoft.com/library/windows/hardware/ff541693)。 **WdfUsbTargetDeviceCreateWithParameters**方法：
    -   客户端驱动程序注册到底层的 USB 驱动程序堆栈。
    -   检索的 WDFUSBDEVICE 句柄由框架创建的 USB 目标设备对象。 模板代码将 USB 目标设备对象的句柄存储在其设备上下文中。 通过使用该句柄，客户端驱动程序可以获取有关设备的特定于 USB 的信息。

    **请注意**  必须调用[ **WdfUsbTargetDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff550077)而不是[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/ff550077withconfig) if、
    -   客户端驱动程序不会调用与 Windows 8 版本的 WDK 一组新的可用 URB 例程。

        如果您的客户端驱动程序调用[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)，USB 驱动程序堆栈假定情况下调用分配所有 URBs [ **WdfUsbTargetDeviceCreateUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439423)或[ **WdfUsbTargetDeviceCreateIsochUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439420)。 分配的这些方法的 URBs 包含由 USB 驱动程序堆栈用于更快地处理的不透明 URB 上下文块。 如果客户端驱动程序使用这些方法都没有分配 URB，USB 驱动程序将生成错误检查。

        有关 URB 分配的详细信息，请参阅[Allocating 和构建 URBs](how-to-add-xrb-support-for-client-drivers.md)。

    -   客户端驱动程序不会遵守的一组规则中所述[最佳实践：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

    此类驱动程序不需要指定客户端约定版本，因此必须跳过步骤 1。

     

3.  选择 USB 配置。

    在模板代码中，选择客户端驱动程序*默认配置*USB 设备中。 默认配置包括配置设备的 0 和每个接口在该配置替代设置 0。

    若要选择的默认配置，客户端驱动程序配置[ **WDF\_USB\_设备\_选择\_配置\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552600)通过调用结构[ **WDF\_USB\_设备\_选择\_配置\_PARAMS\_INIT\_多个\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff552600_init_multiple_interfaces)函数。 该函数初始化**类型**成员添加到**WdfUsbTargetDeviceSelectConfigTypeMultiInterface**以指示，如果多个接口均可用，然后在每个这些设置的替代必须选择接口。 调用必须选择默认配置，因为客户端驱动程序指定中的为 NULL *SettingPairs*参数和 0 *NumberInterfaces*参数。 完成后， **MultiInterface.NumberOfConfiguredInterfaces**的成员**WDF\_USB\_设备\_选择\_配置\_PARAMS**指示为其选择备用设置 0 接口的数量。 不会修改其他成员。

    **请注意**  驱动程序如果客户端驱动程序想要选择备用设置不是默认设置，必须创建的数组[ **WDF\_USB\_接口\_设置\_对**](https://msdn.microsoft.com/library/windows/hardware/ff553023)结构。 数组中的每个元素指定要选择的设备定义的接口数量和替代设置的索引。 信息存储在可以通过调用获取的设备的配置和接口描述符[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550098)方法。 然后，客户端驱动程序必须调用[ **WDF\_USB\_设备\_选择\_配置\_PARAMS\_INIT\_多个\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff552992) ，并将传递**WDF\_USB\_接口\_设置\_对**阵列分区到框架。

     

## <a name="queue-source-code"></a>队列的源代码


*Framework 队列对象*表示特定的框架设备对象的 I/O 队列。 Queue.h 和 Queue.c 中是队列对象的完整源代码。

**Queue.h**

声明由框架的队列对象引发的事件的事件回调例程。

Queue.h 中的第一个块声明队列上下文。

```ManagedCPlusPlus
typedef struct _QUEUE_CONTEXT {

    ULONG PrivateDeviceData;  // just a placeholder

} QUEUE_CONTEXT, *PQUEUE_CONTEXT;

WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(QUEUE_CONTEXT, QueueGetContext)
```

类似于设备上下文，队列上下文是由客户端来存储有关特定队列的信息定义的数据结构。

下面的代码声明 MyUSBDriver\_QueueInitialize 函数，创建并初始化 framework 队列对象的帮助器函数。

```ManagedCPlusPlus
NTSTATUS
MyUSBDriver_QueueInitialize(
    _In_ WDFDEVICE Device
    );
```

下一步的代码示例声明的函数角色类型声明[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)事件回调例程。 事件回调由客户端驱动程序实现，当框架处理设备 I/O 控制请求时调用。

```ManagedCPlusPlus
EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL MyUSBDriver_EvtIoDeviceControl;
```

**Queue.c**

实现文件中，Queue.c，包含以下使用的代码块`alloc_text`杂注指定的驱动程序的实现的 MyUSBDriver\_QueueInitialize 是可分页内存中。

```ManagedCPlusPlus
#ifdef ALLOC_PRAGMA
#pragma alloc_text (PAGE, MyUSBDriver_QueueInitialize)
#endif
```

WDF 提供要处理的请求流到客户端驱动程序的框架队列对象。 当客户端驱动程序调用时，框架将创建 framework 队列对象[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)方法。 在该调用中，客户端驱动程序可以指定某些配置选项之前，框架创建队列。 这些选项包括是否队列是电源管理、 允许的长度为零的请求或是驱动程序的默认队列。 单一框架队列对象可以处理多种类型的请求，如读取、 写入和设备 I/O 控制。 客户端驱动程序可以为这些请求的每个指定事件的回调。

客户端驱动程序还必须指定调度类型。 队列对象的调度类型决定了框架如何提供给客户端驱动程序的请求。 传送机制可以是连续的并行情况下，或由客户端驱动程序定义的自定义机制。 对于顺序队列，直到客户端驱动程序完成上一个请求未传递请求。 在并行调度模式下，框架将请求转发到达从 I/O 管理器时。 这意味着客户端驱动程序可以处理另一个时收到一个请求。 在自定义机制中，客户端手动提取从 framework 队列对象的下一个请求时，驱动程序已准备好对其进行处理。

通常情况下，客户端驱动程序必须设置中的驱动程序的队列[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)事件回调。 模板代码提供了帮助器例程，MyUSBDriver\_QueueInitialize，framework 队列对象初始化。

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

若要设置队列，客户端驱动程序，请执行以下任务：

1.  指定的队列中的配置选项[ **WDF\_IO\_队列\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构。 模板代码使用[ **WDF\_IO\_队列\_CONFIG\_INIT\_默认\_队列**](https://msdn.microsoft.com/library/windows/hardware/ff552359_init_default_queue)函数初始化的结构。 该函数作为默认队列对象指定的队列对象、 是电源管理和并行接收请求。
2.  添加队列的 I/O 请求的客户端驱动程序的事件回调。 在模板中，客户端驱动程序指定一个指向设备 I/O 控制请求其事件回调。
3.  调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)要检索的 WDFQUEUE 句柄由框架创建框架队列对象。

下面是种队列机制的工作原理。 若要与 USB 设备进行通信，应用程序首次打开设备的句柄通过调用**SetDixxx**例程并[ **CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)。 通过使用此句柄，在应用程序调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/hh404258)与特定的控件代码的函数。 根据控制代码的类型，该应用程序可以在该调用中指定输入和输出缓冲区。 最终接收呼叫的 I/O 管理器，然后创建一个请求 (IRP)，并将其转发到客户端驱动程序。 框架截获的请求，创建一个框架请求对象，并将其添加到框架队列对象。 在这种情况下，因为客户端驱动程序已注册设备的 I/O 控制请求其事件回调，该框架将调用的回调。 此外，因为 WdfIoQueueDispatchParallel 标志创建队列对象时，将请求添加到队列时，就立即调用回调。

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

当框架调用客户端驱动程序的事件回调时，会传递一个句柄的 framework 请求对象，用于保存请求 （和其输入和输出缓冲区） 给发送应用程序。 此外，它将一个句柄发送到包含请求的 framework 队列对象。 在事件回叫，客户端驱动程序处理请求根据需要。 模板代码只需完成请求。 客户端驱动程序可以执行更复杂的任务。 例如，如果应用程序请求特定设备的信息，在事件回调，客户端驱动程序可以创建 USB 控制请求并将其发送到 USB 驱动程序堆栈，以便检索请求的设备信息。 中讨论了 USB 控制请求[USB 控制传输](usb-control-transfer.md)。

## <a name="related-topics"></a>相关主题
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  
[WinUSB](winusb.md)  
[编写第一个 USB 客户端驱动程序 (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)  
[编写第一个 USB 客户端驱动程序 (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)  



