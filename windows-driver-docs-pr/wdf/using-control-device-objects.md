---
title: 使用控制设备对象
description: 使用控制设备对象
ms.assetid: 6367954f-6916-46df-a5a0-e80f045b69e5
keywords:
- 控制设备对象 WDK KMDF
- 设备对象 WDK KMDF
- framework 对象 WDK KMDF，控制设备对象
- 旧硬件设备 WDK KMDF
- 仅软件虚拟设备 WDK KMDF
- 系统关闭通知 WDK KMDF
- 关机通知 WDK KMDF
- 通知 WDK KMDF
- 命名 WDK KMDF
- 命名 WDK KMDF，设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2ad389ff85a4ec918802dcf30d5f389edd20ff7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843093"
---
# <a name="using-control-device-objects"></a>使用控制设备对象


*控制设备对象*是不支持即插即用（PnP）或电源管理操作的框架设备对象。 驱动程序可以使用控制设备对象来表示仅限软件的虚拟设备或*旧式硬件设备*（即，不提供 PnP 或电源管理功能的设备）。

创建控制设备对象的驱动程序通常还会为设备对象创建一个符号链接。 应用程序可以通过将符号链接名称传递到 API 元素（例如 Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数），将 i/o 请求发送到控制设备对象。

框架不会将控制设备对象附加到[设备堆栈](wdm-concepts-for-kmdf-drivers.md#device-stacks)。 因此，当应用程序向控制设备对象发送 i/o 请求时，i/o 管理器会直接向创建控制设备对象的驱动程序（而不是堆栈顶部的驱动程序）传递请求。 （但是，附加的驱动程序可以调用[**IoAttachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice) ，以将设备对象附加到控制设备对象的上方。 在这种情况下，附加的驱动程序首先接收 i/o 请求。）

### <a name="uses-of-control-device-objects"></a>使用控制设备对象

控制设备的两个典型用途是：

1.  PnP 设备的筛选器驱动程序（如果驱动程序支持一组用于应用程序的自定义 i/o 控制代码）。

    如果应用程序尝试将自定义 i/o 控制代码发送到驱动程序堆栈的顶部（例如，使用[设备接口](using-device-interfaces.md)的符号链接名称），则筛选器驱动程序上面的驱动程序可能无法在驱动程序无法识别自定义 i/o 控制代码。 若要避免此问题，筛选器驱动程序可以创建控制设备对象。 应用程序可以使用控制设备对象的符号链接名称将 i/o 控制代码直接发送到筛选器驱动程序。

    （请注意，筛选器驱动程序避免此问题的更好方法是充当总线驱动程序并[枚举](enumerating-the-devices-on-a-bus.md)在 raw 模式下操作的子设备。 换句话说，对于筛选器驱动程序支持的每个设备，驱动程序可以创建不需要函数驱动程序的物理设备对象（PDO）。 驱动程序为这些设备调用[**WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)和[**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname) ，并且应用程序可以在发送自定义 i/o 控制代码时按名称标识设备。）

2.  设备的驱动程序，该驱动程序不支持 PnP。

    此类驱动程序必须使用控制设备对象，因为此类设备的设备对象不在设备堆栈中，也不提供 PnP 功能。 有关支持非 PnP 设备的详细信息，请参阅将[内核模式驱动程序框架与非 Pnp 驱动程序配合使用](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)。

### <a name="creating-a-control-device-object"></a>创建控制设备对象

若要创建控制设备对象，驱动程序必须：

1.  调用[**WdfControlDeviceInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)以获取[**WDFDEVICE\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构。

2.  根据需要调用对象初始化方法，以初始化 WDFDEVICE\_INIT 结构。 驱动程序只能调用以下初始化方法：
    -   [**WdfControlDeviceInitSetShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitsetshutdownnotification)
    -   [**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)
    -   [**WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)
    -   [**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)
    -   [**WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)
    -   [**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)
    -   [**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)
    -   [**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)
    -   [**WdfDeviceInitSetIoInCallerContextCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)
    -   [**WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)
    -   [**WdfDeviceInitSetRequestAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)

3.  调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)，它使用 WDFDEVICE\_INIT 结构的内容来创建框架设备对象。

4.  完成以下初始化操作：
    -   如果需要，请为设备[创建默认 i/o 队列](creating-i-o-queues.md)。
    -   如果需要，请调用[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)。
    -   调用[**WdfDeviceCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)可创建应用程序可用来访问控制设备的符号链接名称。

5.  调用[**WdfControlFinishInitializing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)。

### <a name="rules-for-using-control-device-objects"></a>使用控制设备对象的规则

创建控制设备对象的驱动程序必须遵守以下规则：

-   驱动程序无法将控制设备对象的句柄传递给[枚举子设备](enumerating-the-devices-on-a-bus.md)的框架方法。

-   驱动程序无法将控制设备对象的句柄传递给支持[设备接口](using-device-interfaces.md)的框架方法。

-   驱动程序可以创建 i/o 队列并为队列注册请求处理程序，但框架不允许对队列进行[电源管理](using-power-managed-i-o-queues.md)。

-   驱动程序可以为控制设备对象创建[文件对象](framework-file-objects.md)。

### <a name="naming-a-control-device-object"></a>命名控制设备对象

所有控制设备对象都必须命名为。 通常，驱动程序将调用[**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)来分配设备名称，然后调用[**WdfDeviceCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)来创建应用程序可用于访问对象的符号链接名称。

如果你的驱动程序未调用[**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)来分配设备名称，则框架将自动生成控制设备的名称，但你的驱动程序无法调用[**WdfDeviceCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)。

驱动程序可以调用[**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)来指定控制设备的[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)。 设备安装程序类标识注册表的部分，其中包含有关属于安装程序类的设备的管理员提供的信息。 有关调用[**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)的详细信息，请参阅[在基于框架的驱动程序中控制设备访问](controlling-device-access-in-kmdf-drivers.md)。

### <a name="receiving-notification-of-system-shutdown"></a>接收系统关机通知

由于控制设备对象不支持 PnP，因此，驱动程序无法注册回调函数，以便在设备的电源状态发生更改时通知驱动程序。 但是，驱动程序可以调用[**WdfControlDeviceInitSetShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitsetshutdownnotification)来注册[*EvtDeviceShutdownNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification)回调函数。 当系统即将失去其电源时，此回调函数通知驱动程序。

### <a name="deleting-a-control-device-object"></a>删除控制设备对象

在卸载驱动程序之前，某些驱动程序必须删除其控制设备对象，如下所示：

-   如果你的驱动程序创建控制设备对象（不支持 PnP 或电源管理），并且如果驱动程序还创建支持 PnP 和电源管理的框架设备对象，则驱动程序必须最终调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，以 IRQL = 被动\_级别以删除控制设备对象。

    如果驱动程序创建这两种类型的设备对象，则在驱动程序删除控制设备对象之前，操作系统无法卸载驱动程序。

    但是，在框架删除其他设备对象之前，驱动程序不能删除控制设备对象。 若要确定框架删除其他设备对象的时间，驱动程序应为这些对象提供[*EvtCleanupCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)函数。

-   如果你的驱动程序创建了控制设备对象，但未创建支持 PnP 和电源管理的框架设备对象，则驱动程序不必删除控制设备对象。

    在这种情况下，当驱动程序的[*EvtDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)回调函数返回后，框架会删除控制设备对象。

 

 





