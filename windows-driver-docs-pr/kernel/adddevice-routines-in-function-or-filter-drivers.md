---
title: 函数或筛选器驱动程序中的 AddDevice 例程
description: 函数或筛选器驱动程序中的 AddDevice 例程
ms.assetid: 0a095c17-2295-46df-9908-f306f7fe9f67
keywords:
- 函数的驱动程序 WDK 内核
- 筛选器驱动程序 WDK 内核
- AddDevice 例程 WDK 内核功能的驱动程序
- AddDevice 例程 WDK 内核，筛选器驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e81268fadb1224f7c747c621b5643bb3daba98a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365834"
---
# <a name="adddevice-routines-in-function-or-filter-drivers"></a>函数或筛选器驱动程序中的 AddDevice 例程





[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)函数或筛选器驱动程序中的例程应执行以下步骤：

1.  调用[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)创建功能或筛选正添加的设备的设备对象 （FDO 或筛选器执行操作）。

    未指定*DeviceName*设备对象，因为这样做因此跳过的即插即用管理器的安全性。 如果用户模式组件需要到该设备的符号链接，注册的设备接口 （请参阅下面的下一步）。 如果内核模式组件需要旧设备名称，该驱动程序必须将命名的设备对象，但不是建议命名。

    包含文件\_设备\_SECURE\_中打开*DeviceCharacteristics*参数。 这一特性指示要执行安全检查针对的设备对象的所有打开的请求，包括相对打开空格和尾随文件名称将打开的 I/O 管理器。

2.  \[可选\]创建到设备的一个或多个符号链接。

    调用[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)注册设备的功能并创建符号链接，该应用程序或系统组件可用于打开设备。 该驱动程序应启用的界面，通过调用[ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)时，它处理[ **IRP\_MN\_开始\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 有关详细信息，请参阅[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)。

3.  将设备的 PDO 指向存储在设备扩展。

    PnP 管理器提供一个指向作为 PDO *PhysicalDeviceObject*参数*AddDevice*。 驱动程序例程的调用中使用 PDO 指针如[ **IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)。

4.  定义标志中设备的扩展名来跟踪某些即插即用状态的设备，例如设备已暂停，删除，并且意外删除。

    例如，定义一个标志，用于指示设备处于暂停状态时，应保存传入 Irp。 如果驱动程序还没有一种机制的队列 Irp，请创建用于保存 Irp，一个队列。 请参阅[队列和取消排队 Irp](queuing-and-dequeuing-irps.md)有关详细信息。

    此外将分配**IO\_删除\_锁**结构中，设备扩展并调用[ **IoInitializeRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549324)用于初始化此结构。 有关详细信息，请参阅[使用删除锁定](using-remove-locks.md)。

5.  设置了\_缓冲\_IO 或者不要\_直接\_IO 标志位中的设备对象来指定 I/O 管理器是用于发送到设备堆栈的 I/O 请求缓冲的类型。 更高级别的驱动程序或此成员具有相同的值在堆栈中的下一步低驱动程序除外可能是最高级别的驱动程序。 有关详细信息，请参阅[初始化设备对象](initializing-a-device-object.md)。

6.  设置了\_电源\_浪涌或者不要\_POWER\_PAGABLE 标志电源管理，如有必要的。 可分页的驱动程序必须设置 DO\_电源\_PAGABLE 标志。 创建的是 PDO 设备时，总线驱动程序通常会设置设备对象标志。 但是，更高级别的驱动程序可能偶尔需要更改这些标志中的值及其*AddDevice*例程时不创建 FDO 或筛选执行操作。 请参阅[电源管理设置设备对象标志](setting-device-object-flags-for-power-management.md)有关详细信息。

7.  创建和/或初始化该驱动程序使用来管理此设备，如事件、 自旋锁或其他对象的任何其他软件资源。 (在响应中更高版本，配置硬件资源，例如 I/O 端口[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。)

    因为*AddDevice*例程的 IRQL 在系统线程上下文中运行 = 被动\_级别，与分配任何内存[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)供使用以独占方式在初始化期间为页面缓冲池，只要该驱动程序不会控制保存系统页面文件的设备。 必须随此类内存分配[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)之前*AddDevice*返回控件。

8.  将设备对象附加到设备堆栈 ([**IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300))。

    指定一个指向中设备的 PDO*目标设备*参数。

    存储所返回的指针**IoAttachDeviceToDeviceStack**。 This 指针，指向设备下一步较低的驱动程序的设备对象，它是一个必需的参数到[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)并[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)将 Irp 传递设备堆栈的下层时。

9.  清除 DO\_设备\_正在初始化标志 FDO 或筛选器中的执行使用类似于以下语句：

    ```cpp
    FunctionalDeviceObject->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

10. 准备好处理 PnP Irp 的设备 (如[ **IRP\_MN\_查询\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff551715)和**IRP\_MN\_启动\_设备**)。

驱动程序必须启动控制设备，直到收到**IRP\_MN\_启动\_设备**包含的硬件资源分配给设备的即插即用的管理器的列表。

 

 




