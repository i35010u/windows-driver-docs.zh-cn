---
title: WDM 和 WDF 之间的差异
description: WDM 模型与操作系统密切相关。
ms.assetid: 4D35F0AB-44CE-49CA-8AB7-3922871567B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0f1e3cd36aa053cc68ba7f0ed1df13d7d360a4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377413"
---
# <a name="differences-between-wdm-and-wdf"></a>WDM 和 WDF 之间的差异


WDM 模型与操作系统密切相关。 驱动程序通过调用系统服务例程并操作操作系统结构直接与操作系统进行交互。 因为 WDM 驱动程序是受信任的内核模式的组件，系统提供了有限的检查驱动程序的输入。

相比较而言，Windows 驱动程序框架 (WDF) 模型侧重于驱动程序的要求和框架库可处理大多数与系统之间的交互。

框架将截获 I/O 请求、 执行默认操作，在适当的情况并调用所需的驱动程序的回调。 WDF 模型是基于的对象和事件驱动的。 对象表示常见驱动程序构造，例如设备、 锁定或队列。 内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序包含入口点 ([**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers))，所需的服务的事件相关的回调函数设备和支持 I/O 并实现所依赖的任何其他内部实用工具函数。

本部分介绍 WDM 和 WDF 之间的以下区域中的重要区别：

-   [驱动程序结构](#driver-structure)
-   [设备对象和驱动程序角色](#device-objects-and-driver-roles)
-   [对象模型](#object-model)
-   [对象创建](#object-creation)
-   [对象上下文区域](#object-context-area)
-   [受支持的 IRP 类型](#supported-irp-types)
-   [I/O 队列](#io-queues)
-   [同步和并发](#synchronization-and-concurrency)
-   [驱动程序安装](#driver-installation)

## <a name="driver-structure"></a>驱动程序结构


WDM 和 WDF 驱动程序包含[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程、 数例程的调用以处理特定的 I/O 请求，以及各种支持例程。

在 WDM 驱动程序，I/O 调度例程映射到特定的主要 IRP 代码。 调度例程 I/O 管理器从接收 Irp，分析它们，并相应地做出响应。

在 WDF 驱动程序，该框架会注册其自己的调度例程，也不能从 I/O 管理器接收 Irp、 分析它们，然后调用驱动程序的事件回调函数来处理它们。 事件回调函数通常执行比一般的 I/O 调度例程 WDM 驱动程序的更具体的任务。

Plug and Play 设备的典型 WDF 驱动程序包含：

-   一个[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)例程。
-   [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)例程中，这是类似于 WDM AddDevice 例程。
-   一个或多个 I/O 队列。
-   一个或多个 I/O 事件回调函数，它们是在功能上类似于 WDM 驱动程序的 I/O *DispatchXxx*例程。
-   若要处理插和驱动程序支持的电源事件的回调。
-   若要处理的驱动程序支持的 WMI 请求的回调。 （仅限 KMDF）
-   其他回调，相应地，对象清理，文件创建和 I/O 目标，等等。

## <a name="device-objects-and-driver-roles"></a>设备对象和驱动程序角色


WDM 和 WDF 驱动程序创建一个或多个设备对象。 每个设备对象表示目标的输入/输出请求的驱动程序角色。 物理设备对象 (PDO) 表示总线驱动程序、 功能的设备对象 (FDO) 表示功能驱动程序，并筛选设备对象 （筛选器执行操作） 表示筛选器驱动程序。

在 WDM 驱动程序，这些驱动程序角色是隐式的以便该驱动程序必须跟踪每个设备对象表示，并适当地响应 Irp 哪个角色。

WDF 驱动程序，但是，显式指示，一个设备对象表示 PDO (仅 KMDF) FDO，还是筛选器执行操作并注册事件特定于该角色的回调。 例如，PDOs 是目标[资源要求的查询](creating-a-resource-requirements-list.md)和[设备弹出请求](supporting-ejectable-devices.md)，而 DOs FDOs 和筛选器则不处理此类请求。

WDF 驱动程序配置以接收特定类型的 I/O 请求的每个设备对象。 框架调用驱动程序来处理仅这些 I/O 请求并执行默认操作的所有其他请求。 如果设备对象表示筛选器驱动程序，框架会将所有其他请求传递到下一个较低的驱动程序。 如果设备对象表示总线或函数的驱动程序，framework 将失败，其他所有请求类型。

有关插和电源请求，框架调用 KMDF 或 UMDF 驱动程序仅对适用于每个设备对象的请求，并在适当的时间。 例如后已响应基础 PDO, FDO 必须响应某些请求。 WDM 驱动程序，在 FDO 必须将 I/O 完成例程，传递堆栈的下层，IRP，较低的驱动程序后对其进行处理。 WDF 驱动程序只需实现相应的回调例程，并框架低级驱动程序处理完成后调用。

有关如何创建设备对象的框架的信息，请参阅[创建 Framework 设备对象](creating-a-framework-device-object.md)。

某些驱动程序还处理是独立的即插某些 I/O 请求。 WDM 驱动程序将创建一个设备\_对象，如针对此类请求，但不会将它附加到插设备堆栈。 若要完成相同的结果，KMDF 驱动程序[创建一个控制设备对象](using-control-device-objects.md)。 某些基于框架的驱动程序使用来控制设备对象来实现"旁带"I/O 机制，以便它们可以接收特定类型的 I/O 请求，而不考虑设备状态。

## <a name="object-model"></a>对象模型


WDF 支持其中对象是不透明的驱动程序、 提供驱动程序可配置的上下文区域，而引用的句柄的一致的对象模型。 WDM 对象是系统范围内对象的可访问驱动程序，所引用的指针。 损坏了 WDM 对象的驱动程序可能会破坏整个系统。 损坏 WDF 对象不是仅更加困难 — 因为框架验证驱动程序提供的数据，但也会越来越少地导致系统范围内的问题。

有关 KMDF 对象的命名约定的信息，请参阅[WDF 体系结构](kernel-mode-driver-framework-architecture.md)。

框架维护每个对象，因此提供了一定的控制其生存期内的引用计数。 有关详细信息，请参阅[Framework 对象生命周期](framework-object-life-cycle.md)。

尽管许多 WDF 对象对应于 WDM 对象，WDF 对象支持需要 WDM 驱动程序中的其他代码的功能。 WDF 的所有对象，以便将驱动程序可以将存储到具有该对象本身的对象的特定实例相关的信息，都支持驱动程序可定义对象上下文区域。 对象通常跟踪状态，也可以。 例如，WDFQUEUE 对象是不止是一系列输入/输出请求;它们支持多种类型的调度、 与插即用设备，并请求取消的自动同步。 对于 WDFMEMORY 对象 framework 托管引用计数将有助于避免内存泄漏和过早版本的资源。

## <a name="object-creation"></a>对象创建


WDF 驱动程序遵循常规模式来创建所有类型的对象：

1.  如果存在一个，初始化该对象的配置结构。
2.  （可选） 初始化该对象的属性结构。
3.  调用以创建对象的创建方法。

配置结构和属性结构提供有关对象和驱动程序如何使用它的基本信息。 所有对象类型使用[ **WDF\_对象\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)为属性结构，但每种类型的对象的配置结构是不同，某些对象不能有一个。 例如，没有[ **WDF\_驱动程序\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构，但不是**WDF\_设备\_配置**结构。

配置结构存储指向特定于对象的信息，如驱动程序的事件回调函数的对象。 驱动程序填充此结构中，然后调用对象创建方法时将其传递到框架。 例如，调用[ **WdfDriverCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)包括一个指向[ **WDF\_驱动程序\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构，其中包含指向在驱动程序的指针[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。

该框架定义函数被命名为 WDF\_*对象*\_CONFIG\_INIT 来初始化配置结构，其中*对象*表示对象类型的名称。 [ **WDF\_对象\_特性\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdf_object_attributes_init)函数初始化的驱动程序[ **WDF\_对象\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)结构。

## <a name="object-context-area"></a>对象上下文区域


对象的每个实例可以有一个或多个对象上下文区域。 对象上下文区域是用于与该特定实例，如驱动程序分配事件对象相关的数据存储区。 该驱动程序确定的大小和对象上下文区域的布局。 对于设备对象，对象上下文区域是 WDM 设备扩展的等效项。 有关定义和初始化上下文区域的信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

## <a name="supported-irp-types"></a>受支持的 IRP 类型


WDF 支持 Windows Irp 的子集。 主要的 WDM IRP 类型和相应的 WDF 事件回调函数的摘要，请参阅[WDM Irp 和 WDF 事件回调函数](wdm-irps-and-kmdf-event-callback-functions.md)。

即使您的驱动程序未在表中列出的其他接收 Irp，可以将其移植到 KMDF。 KMDF 提供了一种机制，通过该驱动程序可以接收"原始"WDM Irp 但对于其他类型的 Irp 还使用 KMDF 功能。 有关详细信息，请参阅[处理 WDM Irp 之外的框架](handling-wdm-irps-outside-of-the-framework.md)。

## <a name="io-queues"></a>I/O 队列


I/O 请求排队，几乎所有驱动程序。 WDM 驱动程序通常使用以下方法之一：

-   实现[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)函数，并调用[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)并[ **IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)的 I/O 请求中使用系统的设备的队列。
-   使用**IoCsqXxx**或其他列表管理功能来实现其自身内部的 I/O 队列。
-   使用**KeXxxDeviceQueue**函数来初始化和管理保护的旋转锁的队列。

WDF 驱动程序创建 WDF 队列对象 (WDFQUEUE) 来表示 I/O 队列。 WDF 队列对象是类似于取消安全队列，但提供附加功能。

当你移植到 WDF WDM 驱动程序时，可以使用 WDF 排队机制而不考虑 WDM 驱动程序使用的机制。 有关队列的详细信息，请参阅[Framework 队列对象](framework-queue-objects.md)。

## <a name="synchronization-and-concurrency"></a>同步和并发


WDF 驱动程序受益于对 WDM 驱动程序不可用一些内置同步支持。 虽然这种支持并不意味着该驱动程序，可以忽略并发和同步数据访问权限，WDF 驱动程序不过需要明显较少的锁和更少的同步代码比 WDM 驱动程序。

该框架提供的同步功能的详细信息，请参阅[同步技术](synchronization-techniques-for-wdf-drivers.md)。

## <a name="driver-installation"></a>驱动程序安装


WDM 驱动程序，如 KMDF 和 UMDF 驱动程序安装使用 INF 文件。 但是，有时 WDF 驱动程序安装要求的 framework 共同安装程序提供了使用 Windows Driver Kit (WDK)。 辅助安装程序可确保兼容版本的 framework 库的目标系统上存在。 有关安装信息，请参阅[构建和 WDF 驱动程序加载](building-and-loading-a-kmdf-driver.md)。

 

 





