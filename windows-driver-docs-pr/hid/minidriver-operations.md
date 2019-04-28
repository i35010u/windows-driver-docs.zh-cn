---
title: 微型驱动程序和 HID 类驱动程序
description: 操作的 HID 类驱动程序
ms.assetid: 3A8F5545-F8EB-47E2-989D-7DE83E32110E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c9e0ae2cf19ed107445480cef430d4b13a61f02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346217"
---
# <a name="minidrivers-and-the-hid-class-driver"></a>微型驱动程序和 HID 类驱动程序


部分包含有关操作的 HID 类驱动程序的以下主题：

-   操作功能的 HID 类驱动程序
-   绑定到 HID 微型驱动程序的 HID 类驱动程序的操作
-   与 HID 微型驱动程序进行通信

请参阅[创建 WDF HID 微型驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)有关详细信息。

### <a name="operational-features-of-the-hid-class-driver"></a>操作功能的 HID 类驱动程序

HID 类驱动程序将执行以下操作：

-   提供并管理使用内核模式驱动程序和用户模式应用程序的较高级别接口访问[HID 集合](hid-collections.md)输入的设备支持。

    HID 类驱动程序以透明方式管理，并将路由别的驱动程序和应用程序和支持 HID 集合的基础输入的设备之间的所有通信。 它管理的不同的数据由不同的输入设备的协议和支持多个打开的文件，同一 HID 集合上的输入的队列。

    HID 集合的较高级别接口组成[HID 类驱动程序 Ioctl](https://msdn.microsoft.com/library/windows/hardware/ff539849)，则[HIDClass 支持例程](https://msdn.microsoft.com/library/windows/hardware/ff538865)，并[HIDClass 结构](https://msdn.microsoft.com/library/windows/hardware/ff538854)。

-   通过调用微型驱动程序的标准驱动程序例程与 HID 微型驱动程序进行通信。

-   创建功能的设备对象 (*FDO*) 对于 HIDClass 输入设备枚举的较低级别总线或端口驱动程序。

    例如，HID 类驱动程序创建并管理 FDO 表示枚举的系统提供的 USB 驱动程序堆栈的 USB HID 设备的操作。

-   提供子设备 （HID 集合） 的总线驱动程序支持的基础的输入设备的功能。

    HID 类驱动程序创建一个物理设备对象 (*PDO*) 为每个 HID 集合支持的输入设备，并对集合的操作进行管理。

### <a name="binding-a-minidriver-to-hidclass"></a>绑定到 HIDClass 的微型驱动程序

HID 微型驱动程序将其操作绑定到的 HID 类驱动程序，通过调用[ **HidRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff539835)将自身注册 HID 类驱动程序。 注册操作将执行以下操作：

-   将入口点 （指针） 的副本保存到 HID 微型驱动程序的标准驱动程序例程的 HID 类驱动程序的设备扩展中。

    HID 微型驱动程序微型驱动程序收到作为输入的驱动程序对象中设置其入口点及其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。 HID 微型驱动程序设置这些入口点之前注册的 HID 类驱动程序。

-   将微型驱动程序的驱动程序对象中的入口点重置为提供的 HID 类驱动程序的标准驱动程序例程的入口点。

HID 类驱动程序提供以下标准驱动程序例程：

-   [*AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)并[*卸载*](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程

-   以下的 I/O 请求的调度例程：

    [**IRP\_MJ\_CREATE**](https://msdn.microsoft.com/library/windows/hardware/ff550729)

    [**IRP\_MJ\_CLOSE**](https://msdn.microsoft.com/library/windows/hardware/ff550720)

    [**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550744)

    [**IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550766)

    [**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

    [**IRP\_MJ\_SYSTEM\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550813)

注册过程还为 HID mindriver 设备扩展分配内存。 虽然通过 HID 类驱动程序分配内存，但仅 HID 微型驱动程序使用此设备扩展。

### <a name="communicating-with-a-hid-minidriver"></a>与 HID 微型驱动程序进行通信

HID 类驱动程序通过调用 HID 微型驱动程序的 HID 微型驱动程序与通信[ *AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)， [*卸载*](https://msdn.microsoft.com/library/windows/hardware/ff564886)，和调度按如下所示的例程：

### <a name="calling-the-adddevice-routine"></a>调用 AddDevice 例程

当 HID 类驱动程序的**AddDevice**例程调用来创建功能的设备对象 (*FDO*)，HID 类驱动程序创建 FDO，初始化它，并调用 HID 微型驱动程序**AddDevice**例程。 HID 微型驱动程序**AddDevice**例程执行内部的特定于设备的初始化，并在成功后返回状态\_成功。 如果 HID 微型驱动程序**AddDevice**例程不成功，HID 类驱动程序删除 FDO 并返回 HID 微型驱动程序返回的状态**AddDevice**例程。

### <a name="calling-the-unload-routine"></a>调用 Unload 例程

当 HID 类驱动程序**Unload**调用例程，HID 类驱动程序完成释放与 FDO 相关联的所有资源，并调用 HID 微型驱动程序的**卸载**例程。

### <a name="calling-the-dispatch-routines"></a>调用的调度例程

若要运行某个设备，HID 类驱动程序将主要针对内部设备控制请求调用 HID 微型驱动程序调度例程。

此外，当 I/O 管理器可将插、 电源或系统控制请求发送到的 HID 类驱动程序，为 FDO，HID 类驱动程序将处理此请求，并调用 HID 微型驱动程序的相应的调度例程。

HID 类驱动程序不向 HID 微型驱动程序发送以下请求： 创建，请关闭，或设备控制。

### <a name="operation-of-a-hid-minidriver"></a>HID 微型驱动程序的操作

HID 传输微型驱动程序抽象化硬件总线或输入的设备将附加到的端口的操作。

可以使用以下框架的一个内置 HID 微型驱动程序：

-   UMDF – 用户模式驱动程序框架
-   KDMF – 内核模式驱动程序框架
-   WDM – 旧版 Windows 驱动程序模型

Microsoft 建议使用的框架基于解决方案 （KMDF 或 UMDF （在 Windows 8)）。 有关每个驱动程序模型的详细信息，请访问以下各节：

-   基于 KMDF 的 HID 微型驱动程序，请参阅创建框架基于 HID 微型驱动程序
-   基于 UMDF 的 HID 微型驱动程序，请参阅创建 UMDF 基于 HID 微型驱动程序

下的一部分介绍注册 WDM 了基于 HID 微型驱动程序，但其中的许多内容与相关 KMDF 还基于框架驱动程序。 所有的 HID 微型驱动程序必须注册 HID 类驱动程序，以及与微型驱动程序通过调用微型驱动程序的标准驱动程序例程的 HID 类驱动程序通信。

有关 HID 微型驱动程序必须支持在其标准驱动程序例程的功能的详细信息，请参阅以下主题：

-   注册 HID 微型驱动程序
-   HID 微型驱动程序驱动程序扩展
-   使用 HID\_设备\_扩展结构
-   提供的 HID 微型驱动程序的标准驱动程序例程

有关 HID 类驱动程序的详细信息，请参阅的 HID 类驱动程序的操作

### <a name="registering-a-hid-minidriver"></a>注册 HID 微型驱动程序

HID 后微型驱动程序完成中的所有其他驱动程序初始化其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，HID 微型驱动程序将绑定其操作到 HID 类驱动程序通过调用[ **HidRegisterMinidriver**](https://msdn.microsoft.com/library/windows/hardware/ff539835)。

当 HID 微型驱动程序注册与 HID 类驱动程序时，它使用[ **HID\_微型驱动程序\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff539929)结构，以指定以下：HID 的修订、 HID 微型驱动程序驱动程序对象、 HID 微型驱动程序设备扩展的大小和与否是否轮询设备。

### <a name="hid-minidriver-extension"></a>HID 微型驱动程序扩展

HID 微型驱动程序设备扩展是特定于设备，并且仅由 HID 微型驱动程序。 HID 类驱动程序分配的内存的微型驱动程序设备扩展的类驱动程序创建功能的设备对象及其设备扩展时 (*FDO*)。 HID 微型驱动程序时它会向 HID 类驱动程序注册微型驱动程序指定其设备扩展的大小。 通过指定的大小**DeviceExtensionSize**的成员[ **HID\_微型驱动程序\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff539929)结构。

### <a href="" id="using-the-hid-device-extension-structure"></a>使用 HID\_设备\_扩展结构

HID 微型驱动程序必须使用**HID\_设备\_扩展**)。 HID 类驱动程序初始化 FDO 时设置此结构的成员。 HID 微型驱动程序不得更改此结构中的信息。

HID\_设备\_扩展结构包含以下成员：

-   **PhysicalDeviceObject**是指向表示基础输入的设备的物理设备对象 (PDO)。

-   **NextDeviceObject**是指向下方 FDO 设备堆栈的顶部。

-   **MiniDeviceExtension**是指向 HID 微型驱动程序设备扩展。

提供一个指向的输入设备，以下 GET FDO\_微型驱动程序\_设备\_扩展宏将指针返回到 HID 微型驱动程序扩展：

```cpp
#define GET_MINIDRIVER_DEVICE_EXTENSION(DO) ((PDEVICE_EXTENSION) (((PHID_DEVICE_EXTENSION)(DO)->DeviceExtension)->MiniDeviceExtension))
```

PDEVICE\_扩展是指向声明的 HID 微型驱动程序的特定于设备的设备扩展。

同样，HID 微型驱动程序可以获取指向输入的设备的 PDO 和输入的设备 FDO 下设备堆栈的顶部。

当 HID 微型驱动程序将发送设备堆栈的下层 IRP 时，它应使用**NextDeviceObject**作为目标设备对象。

### <a name="standard-minidriver-routines"></a>标准的微型驱动程序例程

HID 微型驱动程序必须提供以下标准驱动程序支持例程：

-   HID 微型驱动程序 DriverEntry 例程
-   HID 微型驱动程序 AddDevice 例程
-   HID 微型驱动程序卸载例程

HID 微型驱动程序还必须支持通过 HID 微型驱动程序调度例程提供中所述的调度例程。

### <a name="driverentry-routine"></a>DriverEntry 例程

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) HID 微型驱动程序中的例程执行以下操作：

-   创建驱动程序 （HID 类驱动程序和 HID 微型驱动程序） 的链接对驱动程序对象。

-   HID 微型驱动程序驱动程序对象中设置所需的驱动程序入口点。

-   调用[ **HidRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff539835) HID 微型驱动程序注册到的 HID 类驱动程序。

-   执行仅供 HID 微型驱动程序的特定于设备的配置。

### <a name="adddevice-routine"></a>AddDevice 例程

HID 类驱动程序处理创建和初始化的功能的设备对象 (*FDO*) 为基础的输入设备。 HID 类驱动程序也表示为基础的设备和其子设备 （HID 集合） 从较高级别接口的角度来看 FDO。

HID 类驱动程序[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程调用 HID 微型驱动程序*AddDevice*这样，微型驱动程序可以执行内部的特定于设备的初始化例程。

传递到 HID 微型驱动程序的参数[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程是微型驱动程序驱动程序对象和 FDO。 (请注意，HID 类驱动程序将 FDO 传递给微型驱动程序*AddDevice*例程，不为基础的输入设备的物理设备对象。)

HID 微型驱动程序[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程从 FDO 微型驱动程序设备扩展到获取的指针。

-   通常情况下，HID 微型驱动程序[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程执行以下操作：

-   初始化微型驱动程序设备扩展。 微型驱动程序只使用设备扩展。

-   返回状态\_成功。 如果微型驱动程序返回了错误状态，HID 类驱动程序删除 FDO，并将返回错误状态插经理。

### <a name="unload-routine"></a>卸载例程

HID 类驱动程序的卸载例程调用 HID 微型驱动程序卸载例程。 HID 微型驱动程序释放分配的微型驱动程序的所有内部资源。

### <a name="dispatch-routines"></a>调度例程

HID 微型驱动程序必须提供以下的调度例程： 创建、 关闭、 内部设备控制、 系统控制、 Plug and Play 和电源管理。 除了内部设备控制请求，大部分这些调度例程提供最小的函数。 当 HID 类驱动程序调用这些调度例程时，传递的微型驱动程序驱动程序对象和功能的设备对象 (*FDO*)。

### <a href="" id="irp-mj-create"></a>IRP\_MJ\_CREATE

符合 WDM 要求情况下，HID 类驱动程序和 HID 微型驱动程序提供的调度例程创建请求。 但是，不能打开 FDO。 HID 类驱动程序将返回状态\_未成功。

HID 微型驱动程序只需提供存根。 永远不会调用创建调度例程。

### <a href="" id="irp-mj-close"></a>IRP\_MJ\_CLOSE

符合 WDM 要求的 HID 类驱动程序和 HID 微型驱动程序必须关闭请求提供的调度例程。 但是，不能打开 FDO。 HID 类驱动程序将返回状态\_无效\_参数\_1。

HID 微型驱动程序只需提供存根。 永远不会调用关闭调度例程。

### <a href="" id="irp-mj-device-control"></a>IRP\_MJ\_设备\_控件

HID 微型驱动程序不需要设备控制请求的调度例程。 HID 类驱动程序不会将设备控制请求传递给微型驱动程序。

### <a href="" id="irp-mj-internal-device-control"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL

HID 微型驱动程序必须为支持中所述的请求的内部设备控制请求提供的调度例程[HID MinidriverIOCTLs](https://msdn.microsoft.com/library/windows/hardware/ff539926)。

HID 类驱动程序主要使用内部设备控制请求来访问基础输入的设备。

HID 微型驱动程序特定于设备的方式处理这些请求。

### <a href="" id="irp-mj-system-control"></a>IRP\_MJ\_系统\_控件

HID 微型驱动程序必须为系统控制请求提供的调度例程。 但是，HID 微型驱动程序只需传递系统控制请求关闭设备堆栈，如下所示：

-   跳过当前的 IRP 堆栈位置

-   发送请求下 FDO 设备堆栈

### <a href="" id="irp-mj-pnp"></a>IRP\_MJ\_PNP

HID 微型驱动程序必须提供插请求的调度例程。

HID 类驱动程序执行与 FDO 相关联的所有即插处理。 当 HID 类驱动程序处理插请求时，它将调用 HID 微型驱动程序插调度例程。

HID 微型驱动程序插调度例程执行以下任务：

-   句柄发送 FDO 设备堆栈关闭请求，并完成请求的方式备份设备堆栈，根据每种类型的请求。

-   执行与特定请求，以更新 FDO 的状态信息关联的特定于设备的处理。

    例如，微型驱动程序可能会更新 FDO 插状态 （特别是，是否 FDO 启动、 停止、 或正被删除）。

### <a href="" id="irp-mj-power"></a>IRP\_MJ\_POWER

HID 微型驱动程序必须提供电源请求的调度例程。 但是，HID 类驱动程序处理 FDO 的处理功能。

符合 WDM 要求 HID 微型驱动程序将关闭 FDO 设备堆栈电源请求发送如下所示：

-   将跳过当前的 IRP 堆栈位置

-   启动下一个幂 IRP

-   将发送 FDO 设备堆栈 IRP 断电

通常情况下，HID 微型驱动程序将传递电源关闭设备堆栈，而无需其他处理的请求。

 

 




