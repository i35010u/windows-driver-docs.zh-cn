---
title: 使用设备接口
description: 使用设备接口
ms.assetid: 98199220-947e-462e-a50c-85d81ca50108
keywords:
- 设备接口 WDK KMDF
- 注册设备接口 WDK KMDF
- 接收设备接口的访问请求 WDK KMDF
- 设备接口的类 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ee21f36a94ac6671e5f6530377bc62c06a610bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326994"
---
# <a name="using-device-interfaces"></a>使用设备接口





一个*设备接口*是符号链接 (PnP) 插到应用程序可用于访问设备的设备。 在用户模式应用程序可以将接口的符号链接名称传递给 API 元素，如 Microsoft Win32 **CreateFile**函数。 若要获取设备接口的符号链接名称，用户模式应用程序可以调用**SetupDi**函数。 有关详细信息**SetupDi**函数，请参阅[使用设备接口函数](https://msdn.microsoft.com/library/windows/hardware/ff553567)。

每个设备接口属于*设备接口类*。 例如，CD-ROM 设备驱动程序堆栈可能会提供一个接口，属于 GUID\_DEVINTERFACE\_CDROM 类。 其中一个光盘设备驱动程序将注册实例的 guid\_DEVINTERFACE\_CDROM 类，以通知系统和应用程序的 CD-ROM 设备已可用。 有关设备接口类的详细信息，请参阅[简介设备接口](https://msdn.microsoft.com/library/windows/hardware/ff549460)。

### <a name="registering-a-device-interface"></a>注册设备接口

若要注册设备接口类的实例，基于框架的驱动程序可以调用[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)中其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。 如果该驱动程序支持的接口的多个实例，它可以为每个实例分配的唯一引用字符串。

该驱动程序已注册设备接口后，该驱动程序可以调用[ **WdfDeviceRetrieveDeviceInterfaceString** ](https://msdn.microsoft.com/library/windows/hardware/ff546842)获取系统具有分配给设备接口的符号链接名称.

驱动程序，可以注册设备接口的其他方法的信息，请参阅[注册设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff549810)。

### <a name="enabling-and-disabling-a-device-interface"></a>启用和禁用设备接口

驱动程序调用后[ **WdfDeviceCreateDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff545935)，框架会自动启用的所有设备的接口时设备将进入其工作状态并禁用这些接口时设备使其处于工作状态。 如果该驱动程序指定一个物理设备对象 (PDO) 时调用它**WdfDeviceCreateDeviceInterface**，如果重新启用已禁用的设备，该框架将重新启用设备的接口。

驱动程序可以禁用和重新启用设备接口，如有必要。 例如，如果驱动程序确定其设备已停止响应，该驱动程序可以调用[ **WdfDeviceSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff546878)以禁用设备的接口和阻止的应用程序获取对接口的新句柄。 （不影响现有的句柄的接口。）如果设备更高版本可用时，该驱动程序可以调用**WdfDeviceSetDeviceInterfaceState**再次以重新启用接口。

### <a name="receiving-requests-to-access-a-device-interface"></a>接收的请求来访问设备接口

应用程序或内核模式组件请求到驱动程序的设备接口的访问时，框架将调用的驱动程序[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)回调函数。 该驱动程序可以调用[ **WdfFileObjectGetFileName** ](https://msdn.microsoft.com/library/windows/hardware/ff547310)若要获取的设备或应用程序或内核模式组件访问的文件的名称。 如果该驱动程序指定引用字符串，它注册的设备接口时，操作系统在文件中包含的引用字符串或设备名称**WdfFileObjectGetFileName**返回。

### <a name="accessing-another-drivers-device-interface"></a>访问另一个驱动程序的设备接口

本部分中显示内核模式驱动程序框架 (KMDF) 驱动程序或用户模式驱动程序框架 (UMDF) 版本 2 驱动程序如何注册的通知到达或另一个驱动程序，提供设备接口的删除，然后创建[远程我/O 目标](general-i-o-targets-in-umdf.md)与设备接口所表示的设备进行通信。

有关如何执行此操作在 UMDF 版本 1 驱动程序中的信息，请参阅[UMDF 驱动程序中使用设备接口](using-device-interfaces-in-umdf-drivers.md#accessing-another-drivers-device-interface)。

若要注册的设备接口事件通知，KMDF 驱动程序调用[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)，而 UMDF 2 驱动程序调用[ **CM\_注册\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh780224)。 在这两种情况下，该驱动程序调用相应例程从其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。

下面的代码示例显示了本地 UMDF 2 驱动程序注册通知的方式，然后打开远程 I/O 目标。

1.  远程驱动程序通过调用注册的设备接口[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)从[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693).
    ```cpp
        UNICODE_STRING ref;
        RtlInitUnicodeString(&ref, MY_HID_FILTER_REFERENCE_STRING);
        status = WdfDeviceCreateDeviceInterface(
                     hDevice,
                     (LPGUID) &GUID_DEVINTERFACE_MY_HIDFILTER_DRIVER,
                     &ref // ReferenceString
                 );

        if (!NT_SUCCESS (status)) {
            MyKdPrint( ("WdfDeviceCreateDeviceInterface failed 0x%x\n", status));
            return status;
        }

    ```

2.  本地驱动程序调用[ **CM\_注册\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh780224)从[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)到当设备接口可用时，请注册通知。 提供指向框架调用设备接口不可用时通知回调例程的指针。
    ```cpp
    DWORD cmRet;
        CM_NOTIFY_FILTER cmFilter;

        ZeroMemory(&cmFilter, sizeof(cmFilter));
        cmFilter.cbSize = sizeof(cmFilter);
        cmFilter.FilterType = CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE;
        cmFilter.u.DeviceInterface.ClassGuid = GUID_DEVINTERFACE_MY_HIDFILTER_DRIVER;

        cmRet = CM_Register_Notification(
                    &cmFilter,                     // PCM_NOTIFY_FILTER pFilter,
                    (PVOID) hDevice,               // PVOID pContext,
                    MyCmInterfaceNotification,    // PCM_NOTIFY_CALLBACK pCallback,
                    &fdoData->CmNotificationHandle // PHCMNOTIFICATION pNotifyContext
                    );
        if (cmRet != CR_SUCCESS) {
            MyKdPrint( ("CM_Register_Notification failed, error %d\n", cmRet));
            status = STATUS_UNSUCCESSFUL;
            return status;
        }   
    ```

3.  系统调用本地驱动程序的通知回调例程每次指定的设备接口到达或已删除。 回调例程可以检查*EventData*参数，以确定哪些设备接口已到达。 然后，它可能队列工作项以打开设备接口。
    ```cpp
    DWORD 
    MyCmInterfaceNotification(
        _In_ HCMNOTIFICATION       hNotify,
        _In_opt_ PVOID             Context,
        _In_ CM_NOTIFY_ACTION      Action,
        _In_reads_bytes_(EventDataSize) PCM_NOTIFY_EVENT_DATA EventData,
        _In_ DWORD                 EventDataSize
        )
    {
        PFDO_DATA fdoData;
        UNICODE_STRING name;
        WDFDEVICE device;
        NTSTATUS status;
        WDFWORKITEM workitem;

        UNREFERENCED_PARAMETER(hNotify);
        UNREFERENCED_PARAMETER(EventDataSize);

        device = (WDFDEVICE) Context;
        fdoData = ToasterFdoGetData(device);

        switch(Action) {
        case CM_NOTIFY_ACTION_DEVICEINTERFACEARRIVAL: 
            MyKdPrint( ("MyCmInterfaceNotification: Arrival of %S\n",
                EventData->u.DeviceInterface.SymbolicLink));

            //
            // Enqueue a work item to open target
            //

            break;
        case CM_NOTIFY_ACTION_DEVICEINTERFACEREMOVAL: 
            MyKdPrint( ("MyCmInterfaceNotification: removal of %S\n",
                EventData->u.DeviceInterface.SymbolicLink));
            break;
        default:
            MyKdPrint( ("MyCmInterfaceNotification: Arrival unknown action\n"));
            break;
        }

        return 0;
    }
    ```


4.  工作项回调函数，从本地驱动程序调用[ **WdfIoTargetCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548591)若要创建远程目标，并[ **WdfIoTargetOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff548634)若要打开远程 I/O 目标。

    调用时[ **WdfIoTargetOpen**](https://msdn.microsoft.com/library/windows/hardware/ff548634)，该驱动程序可以选择注册[ *EvtIoTargetQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff541793)回调函数来接收删除通知，以及有机会拒绝删除。 如果该驱动程序未提供*EvtIoTargetQueryRemove*，框架将关闭 I/O 目标时删除该设备。

    在极少数情况下，UMDF 2 驱动程序可以调用[ **CM\_注册\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh780224)第二次，以注册通知的设备删除。 例如，如果该驱动程序调用[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)若要获取设备接口的句柄，它应注册的设备删除通知，以便它能够正确响应查询删除尝试。 在大多数情况下，UMDF 2 驱动程序将调用**CM\_注册\_通知**仅一次，并且依赖于用于设备删除 WDF 支持。

    ```cpp
    VOID 
    EvtWorkItem(
        _In_ WDFWORKITEM WorkItem
    )
    {
        // 
        // create and open remote target
        //

        return;
    }
    ```

## <a name="related-topics"></a>相关主题

[注册的设备接口到达和设备删除通知](https://msdn.microsoft.com/library/windows/hardware/dn858592)
