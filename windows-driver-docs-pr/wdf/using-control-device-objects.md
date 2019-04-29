---
title: 使用控制设备对象
description: 使用控制设备对象
ms.assetid: 6367954f-6916-46df-a5a0-e80f045b69e5
keywords:
- 控制设备对象 WDK KMDF
- 设备对象 WDK KMDF
- framework 对象 WDK KMDF，控制设备对象
- 旧的硬件设备 WDK KMDF
- 仅限软件的虚拟设备 WDK KMDF
- 系统关闭通知 WDK KMDF
- 关闭通知 WDK KMDF
- 通知 WDK KMDF
- 名称 WDK KMDF
- WDK KMDF，设备对象的名称
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccdd70f979d6822baeb0acb643ec2022a77dc03c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374008"
---
# <a name="using-control-device-objects"></a>使用控制设备对象


一个*控制设备对象*是不支持插即用 (PnP) 或电源管理操作的 framework 设备对象。 驱动程序可用于控制设备对象表示仅限软件的虚拟设备或*原有硬件设备*（即，不提供的设备 PnP 或电源管理功能）。

通常还会创建一个控制设备驱动程序创建的设备对象的符号链接。 应用程序可以通过将符号链接名称传递给 API 元素，如 Microsoft Win32 控件设备对象向发送 I/O 请求[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数。

框架不会附加到控件设备对象[设备堆栈](wdm-concepts-for-kmdf-drivers.md#device-stacks)。 因此，当应用程序发送到控件设备对象的 I/O 请求，I/O 管理器请求将直接传递到控制设备对象，而不是创建到堆栈顶部的驱动程序的驱动程序。 (但是，其他驱动程序可以调用[ **IoAttachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548294)附加控制设备对象上方的设备对象。 在这种情况下，其他驱动程序接收的 I/O 请求第一次。）

### <a name="uses-of-control-device-objects"></a>控制设备对象的用法

用于控制设备的两个典型用途包括：

1.  对于即插即用设备，如果该驱动程序支持自定义应用程序使用的 I/O 控制代码的一组筛选器驱动程序。

    如果应用程序尝试将自定义的 I/O 控制代码发送到驱动程序堆栈的顶部 (例如，使用的符号链接名称[设备接口](using-device-interfaces.md))，上面的筛选器驱动程序的驱动程序可能会失败的 I/O 请求，如果该驱动程序无法识别的自定义的 I/O 控制代码。 若要避免此问题，筛选器驱动程序可以创建一个控制设备对象。 应用程序可用于控制设备对象的符号链接名称 I/O 控制代码将直接发送到筛选器驱动程序。

    (请注意，筛选器驱动程序来避免此问题的更好的方法是作为总线驱动程序和[枚举](enumerating-the-devices-on-a-bus.md)在 raw 模式中运行的子设备。 换而言之，对于每个筛选器驱动程序支持的设备，该驱动程序可以创建不需要功能驱动程序的物理设备对象 (PDO)。 驱动程序调用[ **WdfPdoInitAssignRawDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548802)并[ **WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029)的每个这些设备和应用程序可以识别设备的名称发送自定义的 I/O 控制代码时。）

2.  不支持即插即用设备的驱动程序。

    这样的驱动程序必须使用控件的设备对象，因为此类设备的设备对象不位于设备堆栈并不提供即插即用功能。 支持非 PnP 设备的详细信息，请参阅[非 PnP 驱动程序内核模式驱动程序框架](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)。

### <a name="creating-a-control-device-object"></a>创建控件设备对象

若要创建控制设备对象，驱动程序必须：

1.  调用[ **WdfControlDeviceInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff545841)若要获取[ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。

2.  调用对象的初始化方法，根据需要来初始化 WDFDEVICE\_INIT 结构。 该驱动程序可以调用仅以下初始化方法：
    -   [**WdfControlDeviceInitSetShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff545847)
    -   [**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)
    -   [**WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035)
    -   [**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546043)
    -   [**WdfDeviceInitSetCharacteristics**](https://msdn.microsoft.com/library/windows/hardware/ff546074)
    -   [**WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)
    -   [**WdfDeviceInitSetExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff546097)
    -   [**WdfDeviceInitSetFileObjectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff546107)
    -   [**WdfDeviceInitSetIoInCallerContextCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546119)
    -   [**WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)
    -   [**WdfDeviceInitSetRequestAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff546786)

3.  调用[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)，它使用 WDFDEVICE 内容\_INIT 结构创建 framework 设备对象。

4.  完成以下初始化操作：
    -   [创建默认 I/O 队列](creating-i-o-queues.md)对于设备，如果用户需要一个。
    -   调用[ **WdfDeviceConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff545920)，如果需要。
    -   调用[ **WdfDeviceCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff545939)创建应用程序可用于访问控制设备的符号链接名称。

5.  调用[ **WdfControlFinishInitializing**](https://msdn.microsoft.com/library/windows/hardware/ff545854)。

### <a name="rules-for-using-control-device-objects"></a>使用控件的设备对象的规则

创建设备对象的控件的驱动程序必须遵循下列规则：

-   驱动程序不能通过控制设备对象的句柄到 framework 方法的[枚举子设备](enumerating-the-devices-on-a-bus.md)。

-   驱动程序不能将控制设备对象的句柄传递到支持的框架方法[设备接口](using-device-interfaces.md)。

-   驱动程序可以创建的 I/O 队列并注册请求处理程序的队列，但框架不允许队列要[电源管理](using-power-managed-i-o-queues.md)。

-   驱动程序可以创建[的文件对象](framework-file-objects.md)控制设备对象。

### <a name="naming-a-control-device-object"></a>命名控件设备对象

控制设备的所有对象必须具有都名称。 通常情况下，您的驱动程序将调用[ **WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029)若要分配的设备名称，然后调用[ **WdfDeviceCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff545939)以创建应用程序可用于访问对象的符号链接名称。

如果您的驱动程序不会调用[ **WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029)若要分配的设备名称，框架会自动生成控制设备的名称，但您的驱动程序不能调用[ **WdfDeviceCreateSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff545939)。

您的驱动程序可以调用[ **WdfDeviceInitSetDeviceClass** ](https://msdn.microsoft.com/library/windows/hardware/ff546084)若要指定[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)控制设备。 设备安装程序类标识注册表中包含有关属于的安装程序类的设备的管理员提供信息的一部分。 有关调用详细信息[ **WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)，请参阅[控制基于 Framework 的驱动程序中的设备访问](controlling-device-access-in-kmdf-drivers.md)。

### <a name="receiving-notification-of-system-shutdown"></a>接收通知的系统关闭

控制设备对象不支持即插即用，因为您的驱动程序无法注册设备的电源状态更改时通知该驱动程序的回调函数。 但是，该驱动程序可以调用[ **WdfControlDeviceInitSetShutdownNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff545847)注册[ *EvtDeviceShutdownNotification* ](https://msdn.microsoft.com/library/windows/hardware/ff540911)回调函数。 当系统即将其断电时，此回调函数告知驱动程序。

### <a name="deleting-a-control-device-object"></a>删除控制设备对象

某些驱动程序必须删除驱动程序卸载之前其控制设备对象，如下所示：

-   如果您的驱动程序创建控件 （它不支持即插即用或电源管理） 的设备对象，并且如果该驱动程序还创建框架支持即插即用和电源管理的设备对象，该驱动程序最终必须调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)在 IRQL = 被动\_级别删除控制设备对象。

    如果该驱动程序创建了两种类型的设备对象，操作系统无法卸载您的驱动程序，直到该驱动程序已删除的控制设备对象。

    但是，该驱动程序必须后不删除控制设备对象，直到该框架已删除的其他设备对象。 若要确定何时在 framework 已删除的其他设备对象，您的驱动程序应提供[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)的那些对象的函数。

-   如果您的驱动程序创建设备对象的控件，但不会创建 framework 设备对象的支持即插即用和电源管理驱动程序不需要删除控制设备对象。

    在这种情况下，框架会在驱动程序后删除控制设备对象[ *EvtDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff541694)回调函数返回。

 

 





