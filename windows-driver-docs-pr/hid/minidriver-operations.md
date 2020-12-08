---
title: 微型驱动程序和 HID 类驱动程序
description: HID 类驱动程序的操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9910c1d77549b1182594432f9e29437a884590f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805609"
---
# <a name="minidrivers-and-the-hid-class-driver"></a>微型驱动程序和 HID 类驱动程序


部分包括以下有关 HID 类驱动程序操作的主题：

-   HID 类驱动程序的操作功能
-   将 HID 类驱动程序的操作绑定到 HID 微型驱动程序
-   与 HID 微型驱动程序通信

有关详细信息，请参阅 [创建 WDF HID 微型驱动程序](../wdf/creating-umdf-hid-minidrivers.md) 。

### <a name="operational-features-of-the-hid-class-driver"></a>HID 类驱动程序的操作功能

HID 类驱动程序执行以下操作：

-   提供和管理内核模式驱动程序和用户模式应用程序用来访问输入设备支持的 [HID 集合](hid-collections.md) 的高级界面。

    HID 类驱动程序以透明方式管理并路由上层驱动程序和应用程序与支持 HID 集合的基础输入设备之间的所有通信。 它管理不同的输入设备和输入队列使用的不同数据协议，这些数据协议支持同一 HID 集合上的多个打开的文件。

    HID 类的上层接口包含 [hid 类驱动程序 IOCTLs](/windows-hardware/drivers/ddi/index)、 [HIDClass 支持例程](/windows-hardware/drivers/ddi/index)和 [HIDClass 结构](/windows-hardware/drivers/ddi/index)。

-   通过调用微型驱动程序的标准驱动程序例程与 HID 微型驱动程序通信。

-   为较低级别的总线或端口驱动程序枚举的 HIDClass 输入设备 (*FDO*) 创建一个功能设备对象。

    例如，HID 类驱动程序创建并管理 FDO 的操作，该设备表示由系统提供的 USB 驱动程序堆栈枚举的 USB HID 设备。

-   提供基础设备的总线驱动程序功能，这些设备 (的 HID 集合) 基础输入设备支持。

    HID 类驱动程序为输入设备支持的每个 HID 集合创建一个物理设备对象 (*PDO*) ，并管理集合的操作。

### <a name="binding-a-minidriver-to-hidclass"></a>将微型驱动程序绑定到 HIDClass

HID 微型驱动程序通过调用 [**HidRegisterMinidriver**](/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver) 将其自身注册到 hid 类驱动程序，将其操作绑定到 hid 类驱动程序。 注册操作执行以下操作：

-   将 (指针) 入口点副本保存到 HID 类驱动程序的设备扩展中的 HID 微型驱动程序标准驱动程序例程。

    HID 微型驱动程序设置驱动程序对象中的入口点，微型驱动程序将其作为输入接收到其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 HID 微型驱动程序在向 HID 类驱动程序注册之前设置这些入口点。

-   将微型驱动程序的驱动程序对象中的入口点重置为 HID 类驱动程序提供的标准驱动程序例程的入口点。

HID 类驱动程序提供以下标准驱动程序例程：

-   [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 和 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程

-   以下 i/o 请求的调度例程：

    [**IRP \_ MJ \_ 创建**](../kernel/irp-mj-create.md)

    [**IRP \_ MJ \_ 关闭**](../kernel/irp-mj-close.md)

    [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)

    [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)

    [**IRP \_ MJ \_ PNP**](../kernel/irp-mj-pnp.md)

    [**IRP \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)

注册过程还会为 HID mindriver 设备扩展分配内存。 尽管内存由 HID 类驱动程序分配，但只有 HID 微型驱动程序使用此设备扩展。

### <a name="communicating-with-a-hid-minidriver"></a>与 HID 微型驱动程序通信

HID 类驱动程序通过调用 HID 微型驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)、 [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)和调度例程与 hid 微型驱动程序通信，如下所示：

### <a name="calling-the-adddevice-routine"></a>调用 AddDevice 例程

当调用 HID 类驱动程序的 **AddDevice** 例程来创建)  (*FDO* 的功能设备对象时，HID 类驱动程序将创建 FDO，对其进行初始化，并调用 HID 微型驱动程序 **AddDevice** 例程。 HID 微型驱动程序 **AddDevice** 例程执行特定于设备的内部初始化，如果成功，则返回状态 " \_ 成功"。 如果 HID 微型驱动程序 **AddDevice** 例程不成功，则 hid 类驱动程序将删除 FDO 并返回 HID 微型驱动程序 **AddDevice** 例程返回的状态。

### <a name="calling-the-unload-routine"></a>调用 Unload 例程

调用 HID 类驱动程序 **卸载** 例程后，hid 类驱动程序将完成与 FDO 关联的所有资源，并调用 HID 微型驱动程序的 **卸载** 例程。

### <a name="calling-the-dispatch-routines"></a>调用调度例程

为操作设备，HID 类驱动程序主要为内部设备控制请求调用 HID 微型驱动程序调度例程。

此外，当 i/o 管理器将即插即用、电源或系统控制请求发送到 FDO 的 HID 类驱动程序时，HID 类驱动程序会处理请求，并调用 HID 微型驱动程序的相应调度例程。

HID 类驱动程序不会将以下请求发送到 HID 微型驱动程序： create、close 或 device control。

### <a name="operation-of-a-hid-minidriver"></a>HID 微型驱动程序的操作

HID 传输微型驱动程序抽象了输入设备附加到的硬件总线或端口的操作。

可以使用以下框架之一生成 HID 微型驱动程序：

-   UMDF –用户模式驱动程序框架
-   KDMF –内核模式驱动程序框架
-   WDM –旧 Windows 驱动模型

Microsoft 建议仅在 Windows 8 上使用基于框架的解决方案 (KMDF 或 UMDF (，) # A3。 有关每个驱动程序模型的详细信息，请访问以下各节：

-   KMDF HID 微型驱动程序，请参阅创建基于框架的 HID 微型驱动程序
-   基于 UMDF 的 HID 微型驱动程序，请参阅创建基于 UMDF 的 HID 微型驱动程序

以下部分介绍了如何注册基于 WDM 的 HID 微型驱动程序，但其中的许多内容也涉及到基于 KMDF 的框架驱动程序。 所有 HID 微型驱动程序都必须注册到 HID 类驱动程序，并且 HID 类驱动程序通过调用微型驱动程序的标准驱动程序例程与微型驱动程序通信。

有关 HID 微型驱动程序在其标准驱动程序例程中必须支持的功能的详细信息，请参阅以下主题：

-   注册 HID 微型驱动程序
-   HID 微型驱动程序驱动程序扩展
-   使用 HID \_ 设备 \_ 扩展结构
-   HID 微型驱动程序提供的标准驱动程序例程

有关 HID 类驱动程序的详细信息，请参阅 HID 类驱动程序的操作

### <a name="registering-a-hid-minidriver"></a>注册 HID 微型驱动程序

当 HID 微型驱动程序在其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程中完成所有其他驱动程序初始化后，hid 微型驱动程序通过调用 [**HidRegisterMinidriver**](/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)将其操作绑定到 HID 类驱动程序。

当 HID 微型驱动程序注册到 HID 类驱动程序时，它使用 [**hid \_ 微型驱动程序 \_ 注册**](/windows-hardware/drivers/ddi/hidport/ns-hidport-_hid_minidriver_registration) 结构来指定以下各项： hid 版本、hid 微型驱动程序驱动程序对象、hid 微型驱动程序设备扩展的大小以及是否轮询设备。

### <a name="hid-minidriver-extension"></a>HID 微型驱动程序扩展

HID 微型驱动程序设备扩展是特定于设备的，仅供 HID 微型驱动程序使用。 类驱动程序为功能设备对象创建其设备扩展 (*FDO*) 时，HID 类驱动程序为微型驱动程序设备扩展分配内存。 在将微型驱动程序注册到 HID 类驱动程序时，HID 微型驱动程序指定其设备扩展的大小。 该大小由 [**HID \_ 微型驱动程序 \_ 注册**](/windows-hardware/drivers/ddi/hidport/ns-hidport-_hid_minidriver_registration)结构的 **DeviceExtensionSize** 成员指定。

### <a name="using-the-hid_device_extension-structure"></a><a href="" id="using-the-hid-device-extension-structure"></a>使用 HID \_ 设备 \_ 扩展结构

HID 微型驱动程序必须使用 [**hid \_ 设备 \_ 扩展**](/windows-hardware/drivers/ddi/hidport/ns-hidport-_hid_device_extension) 结构 *作为) 的* 功能设备 (对象的 hid 类驱动程序所创建的设备扩展的布局。 HID 类驱动程序在初始化 FDO 时设置此结构的成员。 HID 微型驱动程序不能更改此结构中的信息。

HID \_ 设备 \_ 扩展结构包含以下成员：

-   **PhysicalDeviceObject** 是一个指针，指向表示基础输入设备 (PDO) 的物理设备对象。

-   **NextDeviceObject** 是一个指针，指向 FDO 下的设备堆栈顶部。

-   **MiniDeviceExtension** 是指向 HID 微型驱动程序设备扩展的指针。

给定一个指向输入设备的 FDO 的指针，以下 GET \_ 微型驱动程序 \_ 设备 \_ 扩展宏将返回指向 HID 微型驱动程序扩展的指针：

```cpp
#define GET_MINIDRIVER_DEVICE_EXTENSION(DO) ((PDEVICE_EXTENSION) (((PHID_DEVICE_EXTENSION)(DO)->DeviceExtension)->MiniDeviceExtension))
```

PDEVICE \_ EXTENSION 是一个指针，指向由 HID 微型驱动程序声明的特定于设备的设备扩展。

同样，HID 微型驱动程序可以获取指向输入设备的 PDO 的指针，以及输入设备 FDO 下的设备堆栈的顶部。

当 HID 微型驱动程序将 IRP 发送到设备堆栈时，它应使用 **NextDeviceObject** 作为目标设备对象。

### <a name="standard-minidriver-routines"></a>标准微型驱动程序例程

HID 微型驱动程序必须提供以下标准驱动程序支持例程：

-   HID 微型驱动程序 DriverEntry 例程
-   HID 微型驱动程序 AddDevice 例程
-   HID 微型驱动程序卸载例程

HID 微型驱动程序还必须支持 HID 微型驱动程序提供的调度例程中所述的调度例程。

### <a name="driverentry-routine"></a>DriverEntry 例程

HID 微型驱动程序中的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程执行以下操作：

-   为链接的驱动程序对 (HID 类驱动程序和 HID 微型驱动程序) 创建驱动程序对象。

-   在 HID 微型驱动程序驱动程序对象中设置所需的驱动程序入口点。

-   调用 [**HidRegisterMinidriver**](/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver) ，将 hid 微型驱动程序注册到 hid 类驱动程序。

-   仅供 HID 微型驱动程序使用的设备特定配置。

### <a name="adddevice-routine"></a>AddDevice 例程

HID 类驱动程序处理为基础输入设备 (*FDO*) 创建和初始化功能设备对象。 HID 类驱动程序还会将 FDO 从顶级接口的角度操作到基础设备，并将其子设备 (HID 集合) 。

HID 类 driver [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程调用 Hid 微型驱动程序 *AddDevice* 例程，使微型驱动程序可以执行特定于设备的初始化。

传递给 HID 微型驱动程序 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程的参数是微型驱动程序驱动程序对象和 FDO。  (请注意，HID 类驱动程序将 FDO 传递到微型驱动程序 *AddDevice* 例程，而不是基础输入设备的物理设备对象。 ) 

HID 微型驱动程序 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程从 FDO 获取指向微型驱动程序设备扩展的指针。

-   通常，HID 微型驱动程序 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程会执行以下操作：

-   初始化微型驱动程序设备扩展。 设备扩展仅由微型驱动程序使用。

-   返回状态 " \_ 成功"。 如果微型驱动程序返回错误状态，则 HID 类驱动程序将删除 FDO，并将错误状态返回到即插即用管理器。

### <a name="unload-routine"></a>卸载例程

HID 类驱动程序的卸载例程调用 HID 微型驱动程序 Unload 例程。 HID 微型驱动程序释放由微型驱动程序分配的任何内部资源。

### <a name="dispatch-routines"></a>调度例程

HID 微型驱动程序必须提供以下调度例程：创建、关闭、内部设备控制、系统控制、即插即用和电源管理。 除了内部设备控制请求以外，其中的大多数调度例程均提供最小功能。 当 HID 类驱动程序调用这些调度例程时，它会将微型驱动程序驱动程序对象和功能设备对象传递 (*FDO*) 。

### <a name="irp_mj_create"></a><a href="" id="irp-mj-create"></a>IRP \_ MJ \_ 创建

与 WDM 要求兼容，HID 类驱动程序和 HID 微型驱动程序为创建请求提供调度例程。 但是，无法打开 FDO。 HID 类驱动程序返回状态 "未 \_ 成功"。

HID 微型驱动程序只需提供存根。 永远不会调用 create 调度例程。

### <a name="irp_mj_close"></a><a href="" id="irp-mj-close"></a>IRP \_ MJ \_ 关闭

在符合 WDM 要求的情况下，HID 类驱动程序和 HID 微型驱动程序必须为关闭请求提供调度例程。 但是，无法打开 FDO。 HID 类驱动程序返回状态 \_ 无效 \_ 参数 \_ 1。

HID 微型驱动程序只需提供存根。 永远不会调用关闭调度例程。

### <a name="irp_mj_device_control"></a><a href="" id="irp-mj-device-control"></a>IRP \_ MJ \_ 设备 \_ 控制

HID 微型驱动程序不需要设备控制请求的调度例程。 HID 类驱动程序不会将设备控制请求传递给微型驱动程序。

### <a name="irp_mj_internal_device_control"></a><a href="" id="irp-mj-internal-device-control"></a>IRP \_ MJ \_ 内部 \_ 设备 \_ 控制

HID 微型驱动程序必须为支持 [HID MinidriverIOCTLs](/windows-hardware/drivers/ddi/index)中所述请求的内部设备控制请求提供调度例程。

HID 类驱动程序主要使用内部设备控制请求来访问基础输入设备。

HID 微型驱动程序以设备特定的方式处理这些请求。

### <a name="irp_mj_system_control"></a><a href="" id="irp-mj-system-control"></a>IRP \_ MJ \_ 系统 \_ 控件

HID 微型驱动程序必须为系统控制请求提供调度例程。 但是，只需使用 HID 微型驱动程序按如下所示将系统控制请求传递到设备堆栈：

-   跳过当前 IRP 堆栈位置

-   向下发送请求 FDO 的设备堆栈

### <a name="irp_mj_pnp"></a><a href="" id="irp-mj-pnp"></a>IRP \_ MJ \_ PNP

HID 微型驱动程序必须为即插即用请求提供调度例程。

HID 类驱动程序将执行与 FDO 关联的所有即插即用处理。 当 HID 类驱动程序处理即插即用请求时，它将调用 HID 微型驱动程序即插即用调度例程。

HID 微型驱动程序即插即用调度例程执行以下操作：

-   按照适用于每种类型的请求，处理 FDO 的设备堆栈中发送请求的方式，并按备份设备堆栈的方式完成请求。

-   与特定的请求关联的特定于设备的处理，以更新有关 FDO 状态的信息。

    例如，微型驱动程序可能会更新 FDO (的即插即用状态，具体而言，无论是启动、停止还是在) 删除该 FDO。

### <a name="irp_mj_power"></a><a href="" id="irp-mj-power"></a>IRP \_ MJ \_ POWER

HID 微型驱动程序必须为电源请求提供调度例程。 但是，HID 类驱动程序处理 FDO 的电源处理。

与 WDM 要求兼容时，HID 微型驱动程序通过以下方式向 FDO 的设备堆栈下发送电源请求：

-   跳过当前 IRP 堆栈位置

-   启动下一个 power IRP

-   将电源 IRP 向下发送到 FDO 的设备堆栈

通常情况下，HID 微型驱动程序无需额外处理即可将电源请求向下传递到设备堆栈中。

