---
title: WDM 和 WDF 之间的差异
description: WDM 模型与操作系统密切相关。
ms.assetid: 4D35F0AB-44CE-49CA-8AB7-3922871567B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e36ca7e43cc8f83a88907fc3b0eb11db98aa4e2f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183947"
---
# <a name="differences-between-wdm-and-wdf"></a>WDM 和 WDF 之间的差异


WDM 模型与操作系统密切相关。 驱动程序通过调用系统服务例程和操作操作系统结构，直接与操作系统交互。 由于 WDM 驱动程序是受信任的内核模式组件，因此系统对驱动程序输入提供有限的检查。

相比之下，Windows 驱动程序框架 (WDF) 模型注重驱动程序的要求，框架库处理与系统的大多数交互。

框架截获 i/o 请求，在适当的位置采取默认操作，并根据需要调用驱动程序的回调。 WDF 模型是基于对象的和事件驱动的。 对象表示常用驱动程序构造，如设备、锁定或队列。 内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 驱动程序包含一个入口点 ([**DriverEntry**](./driverentry-for-kmdf-drivers.md)) 、为设备提供服务和支持 i/o 所需的与事件相关的回调函数，以及实现所依赖的任何其他内部实用工具函数。

本部分介绍了以下几个方面的 WDM 与 WDF 之间的重要差异：

-   [驱动程序结构](#driver-structure)
-   [设备对象和驱动程序角色](#device-objects-and-driver-roles)
-   [对象模型](#object-model)
-   [对象创建](#object-creation)
-   [对象上下文区域](#object-context-area)
-   [支持的 IRP 类型](#supported-irp-types)
-   [I/o 队列](#io-queues)
-   [同步和并发](#synchronization-and-concurrency)
-   [驱动程序安装](#driver-installation)

## <a name="driver-structure"></a>驱动程序结构


WDM 和 WDF 驱动程序都包含 [**DriverEntry**](./driverentry-for-kmdf-drivers.md) 例程、用于处理特定 i/o 请求的许多例程以及各种支持例程。

在 WDM 驱动程序中，i/o 调度例程映射到特定的主要 IRP 代码。 调度例程从 i/o 管理器接收 Irp，对其进行分析，并相应地做出响应。

在 WDF 驱动程序中，该框架将注册自己的调度例程，该例程从 i/o 管理器接收 Irp，对其进行分析，然后调用驱动程序的事件回调函数来处理它们。 与 WDM 驱动程序的常规 i/o 调度例程相比，事件回调函数执行的任务通常更为具体。

即插即用设备的典型 WDF 驱动程序包含：

-   [**DriverEntry**](./driverentry-for-kmdf-drivers.md)例程。
-   [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)例程，在功能上类似于 WDM AddDevice 例程。
-   一个或多个 i/o 队列。
-   一个或多个 i/o 事件回调函数，这些函数在函数中与 WDM 驱动程序的 i/o *DispatchXxx* 例程类似。
-   用于处理驱动程序支持的即插即用和电源事件的回调。
-   用于处理驱动程序支持的 WMI 请求的回调。  (KMDF-仅) 
-   其他回调，适用于对象清理、文件创建和 i/o 目标等。

## <a name="device-objects-and-driver-roles"></a>设备对象和驱动程序角色


WDM 和 WDF 驱动程序都创建一个或多个设备对象。 每个设备对象表示作为 i/o 请求的目标的驱动程序角色。  (PDO) 的物理设备对象表示总线驱动程序、功能设备对象 (FDO) 表示函数驱动程序，筛选器设备对象 (筛选器) 表示筛选器驱动程序。

在 WDM 驱动程序中，这些驱动程序角色是隐式的，因此，驱动程序必须跟踪每个设备对象表示的角色，并对 Irp 做出相应的响应。

但是，WDF 驱动程序明确表示设备对象是否表示一个 PDO (仅) 、FDO 或筛选器执行并注册特定于该角色的事件回调。 例如，PDOs 是 [资源需求查询](creating-a-resource-requirements-list.md) 和 [设备弹出请求](supporting-ejectable-devices.md)的目标，而 FDOs 和 filter DOs 不处理此类请求。

WDF 驱动程序将每个设备对象配置为接收特定类型的 i/o 请求。 框架调用驱动程序来仅处理这些 i/o 请求，并对所有其他请求执行默认操作。 如果设备对象表示筛选器驱动程序，框架会将所有其他请求传递到下一个较低的驱动程序。 如果设备对象表示总线或函数驱动程序，则该框架将无法满足所有其他请求类型的要求。

对于即插即用和电源请求，框架只为适用于每个设备对象的请求调用 KMDF 或 UMDF 驱动程序，并在适当的时间调用该驱动程序。 例如，在基础 PDO 已响应后，FDO 必须响应某些请求。 在 WDM 驱动程序中，FDO 必须设置 i/o 完成例程，将 IRP 向下传递到堆栈，然后在较低的驱动程序之后对其进行处理。 WDF 驱动程序只是实现相应的回调例程，并且框架在较低的驱动程序完成处理后调用它。

有关如何创建框架设备对象的信息，请参阅 [创建框架设备对象](creating-a-framework-device-object.md)。

某些驱动程序还处理与即插即用无关的特定 i/o 请求。 WDM 驱动程序创建设备 \_ 对象作为此类请求的目标，但不将其附加到即插即用设备堆栈。 若要实现相同的结果，KMDF 驱动程序将 [创建一个控制设备对象](using-control-device-objects.md)。 某些基于框架的驱动程序使用控制设备对象来实现 "sideband" i/o 机制，以便它们可以接收特定类型的 i/o 请求，而不考虑设备状态。

## <a name="object-model"></a>对象模型


WDF 支持连贯对象模型，在该模型中，对象在驱动程序中是不透明的，提供驱动程序可配置的上下文区域，并由句柄引用。 WDM 对象是系统范围内的对象，这些对象可由驱动程序访问并由指针引用。 损坏 WDM 对象的驱动程序可能会损坏整个系统。 损坏 WDF 对象不仅更难，因为框架会验证驱动程序提供的数据，但也会导致系统范围内的问题不太频繁。

有关 KMDF 对象的命名约定的信息，请参阅 [WDF 体系结构](kernel-mode-driver-framework-architecture.md)。

框架维护每个对象的引用计数，从而提供对其生存期的一些控制。 有关详细信息，请参阅 [框架对象生命周期](framework-object-life-cycle.md)。

尽管很多 WDF 对象对应于 WDM 对象，但 WDF 对象支持在 WDM 驱动程序中需要其他代码的功能。 所有 WDF 对象均支持驱动程序可定义的对象上下文区域，以便驱动程序可以将与对象的特定实例相关的信息存储到对象本身。 对象通常也跟踪状态。 例如，WDFQUEUE 对象不仅仅是 i/o 请求的列表;它们支持多种调度类型、自动同步与即插即用和请求取消。 对于 WDFMEMORY 对象，框架托管的引用计数有助于防止内存泄漏和资源的过早发布。

## <a name="object-creation"></a>对象创建


WDF 驱动程序遵循定期模式来创建所有类型的对象：

1.  初始化对象的配置结构（如果存在）。
2.  可以选择初始化对象的属性结构。
3.  调用创建方法来创建对象。

配置结构和属性结构提供有关对象的基本信息以及驱动程序如何使用该对象。 所有对象类型都使用 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 作为属性结构，但每种类型的对象的配置结构都不同，某些对象没有。 例如，有一个 [**wdf \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config) 结构，但不是 **wdf \_ 设备 \_ 配置** 结构。

配置结构保存指向对象特定信息的指针，如驱动程序的对象的事件回调函数。 驱动程序将填充此结构，然后在调用对象创建方法时将其传递到框架。 例如，对 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 的调用包括一个指向 [**WDF \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config) 结构的指针，该结构包含指向驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数的指针。

框架定义名为 WDF \_ *对象* \_ CONFIG \_ INIT 的函数以初始化配置结构，其中*对象*表示对象类型的名称。 [**WDF \_ 对象 \_ 属性 \_ INIT**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)函数初始化驱动程序的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构。

## <a name="object-context-area"></a>对象上下文区域


对象的每个实例都可以有一个或多个对象上下文区。 对象上下文区域是与特定实例相关的数据的存储区域，如驱动程序分配的事件对象。 驱动程序确定对象上下文区域的大小和布局。 对于设备对象，对象上下文区等效于 WDM 设备扩展。 有关定义和初始化上下文区域的信息，请参阅 [框架对象上下文空间](framework-object-context-space.md)。

## <a name="supported-irp-types"></a>支持的 IRP 类型


WDF 支持 Windows Irp 的一个子集。 有关主要 WDM IRP 类型和相应的 WDF 事件回调函数的摘要，请参阅 [WDM irp 和 Wdf 事件回调函数](wdm-irps-and-kmdf-event-callback-functions.md)。

即使您的驱动程序收到的是表中列出的 Irp 以外的其他 Irp，也可以将其移植到 KMDF。 KMDF 提供了一种机制，通过该机制，驱动程序可以接收 "原始" WDM Irp，但也可以对其他类型的 Irp 使用 KMDF 功能。 有关详细信息，请参阅 [在框架外处理 WDM irp](handling-wdm-irps-outside-of-the-framework.md)。

## <a name="io-queues"></a>I/o 队列


几乎所有驱动程序都排队 i/o 请求。 WDM 驱动程序通常使用以下方法之一：

-   实现 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 函数并调用 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) 和 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) ，以将系统的设备队列用于 i/o 请求。
-   使用 **IoCsqXxx** 或其他列表管理功能来实现其自己的内部 i/o 队列。
-   使用 **KeXxxDeviceQueue** 函数可初始化和管理由旋转锁保护的队列。

WDF 驱动程序创建一个 WDF 队列对象 (WDFQUEUE) 来表示 i/o 队列。 WDF 队列对象类似于取消安全队列，但提供其他功能。

将 WDM 驱动程序移植到 WDF 时，可以使用 WDF 队列机制，而无需考虑 WDM 驱动程序使用的机制。 有关队列的详细信息，请参阅 [框架队列对象](framework-queue-objects.md)。

## <a name="synchronization-and-concurrency"></a>同步和并发


WDF 驱动程序得益于无法用于 WDM 驱动程序的某些内置同步支持。 尽管此支持并不意味着驱动程序可以忽略并发数据访问和同步访问数据，但是 WDF 驱动程序所需的锁和的同步代码比 WDM 驱动程序要少得多。

有关框架提供的同步功能的详细信息，请参阅 [同步技术](./using-automatic-synchronization.md)。

## <a name="driver-installation"></a>驱动程序安装


与 WDM 驱动程序一样，KMDF 和 UMDF 驱动程序使用 INF 文件进行安装。 但是，WDF 驱动程序安装有时需要随 Windows 驱动程序工具包一起提供的框架共同安装程序 (WDK) 。 共同安装程序可确保目标系统上存在框架库的兼容版本。 有关安装的信息，请参阅 [生成和加载 WDF 驱动程序](building-and-loading-a-kmdf-driver.md)。

 

