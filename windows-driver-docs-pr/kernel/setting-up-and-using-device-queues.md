---
title: 设置和使用设备队列
description: 设置和使用设备队列
ms.assetid: 5221ffc0-0cb4-498b-9be2-4d240b5f2744
keywords:
- 设备队列 WDK Irp，设置
- 设备队列 WDK Irp，对象
- 在队列中插入 Irp
- 存储设备队列对象
- 补充 IRP 队列 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54294a7b37a30053b879193607d3dd8923029378
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325027"
---
# <a name="setting-up-and-using-device-queues"></a>设置和使用设备队列





驱动程序设置的设备队列对象通过调用[ **KeInitializeDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552126)在驱动程序或设备的初始化。 启动其设备之后, 该驱动程序将 Irp 插入此队列通过调用[ **KeInsertDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552180)或[ **KeInsertByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552178). 下图说明了这些调用。

![设置和使用设备队列](images/3devqobj.png)

如此图所示，该驱动程序必须提供设备队列对象，它必须是驻留的存储。 通常设置的设备队列对象的驱动程序提供必要的存储中[设备扩展](device-extensions.md)驱动程序创建的设备的对象，但存储可以是在控制器扩展如果驱动程序使用[控制器对象](using-controller-objects.md)或非分页缓冲池分配驱动程序中。

如果驱动程序提供了存储设备扩展中的设备队列对象，则会调用**KeInitializeDeviceQueue**之后创建的设备对象和之前启动设备。 换而言之，驱动程序可以初始化队列从其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程或它处理即插即用[ **IRP\_MN\_开始\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 在调用**KeInitializeDeviceQueue**，驱动程序将指针传递给它提供有关设备队列对象的存储。

启动其设备之后, 该驱动程序可以插入 IRP 到其设备的队列通过调用**KeInsertDeviceQueue**，其中放置于队列的尾部 IRP 或**KeInsertByKeyDeviceQueue**、 哪些置于根据驱动程序确定队列 IRP *SortKey*值，如在上图中所示。

每种支持例程返回一个布尔值，该值 IRP 已插入到队列。 其中每个调用还设置到繁忙的设备队列对象的状态队列当前是否为空 （不繁忙）。 但是，如果队列为空 （不忙），两者**KeInsert*Xxx*DeviceQueue**例程将 IRP 插入到队列。 相反，它的设备队列对象的状态设置为繁忙，并返回**FALSE**。 由于 IRP 不排入队列，该驱动程序必须将其传递到另一个驱动程序例程进行进一步处理。

**在设置补充设备队列，请按照本实现原则：**

在调用**KeInsert*Xxx*DeviceQueue**返回**FALSE**，调用方必须传递它尝试在对队列的进一步处理到另一个驱动程序例程 IRP。
但是，在调用**KeInsert*Xxx*DeviceQueue**设备队列对象的状态更改为繁忙、，以便在下一步 IRP 插入队列中，除非该驱动程序调用**KeRemove*Xxx*DeviceQueue**第一个。

当设备队列对象的状态设置为繁忙时，驱动程序可以取消 IRP 排队进行进一步处理或将状态重置为不忙，通过调用以下支持例程之一：

-   [**KeRemoveDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553156)若要删除队列的开头处 IRP

-   [**KeRemoveByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553152)若要删除选择根据驱动程序确定 IRP *SortKey*值

-   [**KeRemoveEntryDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553163)队列中删除特定 IRP 或确定队列是否为特定 IRP

    **KeRemoveEntryDeviceQueue**返回一个布尔值，该值指示 IRP 设备队列中。

调用这些例程，以从为空但繁忙的设备队列中删除项的任何更改为不忙的队列状态。

每个设备队列对象受内置 executive 旋转锁 (不会显示[使用设备队列对象](#setting-up-and-using-device-queues)图)。 因此，驱动程序可以将 Irp 插入到队列和从正在运行在更短于或等于 IRQL 的任何驱动程序例程以包含多个处理器安全的方式删除它们 = 调度\_级别。 由于存在此 IRQL 限制，驱动程序不能调用任何**Ke*Xxx*DeviceQueue**例程从其 ISR 或[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)例程在 DIRQL 运行。

请参阅[管理硬件优先级](managing-hardware-priorities.md)并[旋转锁](spin-locks.md)有关详细信息。 为特定的支持例程的 IRQL 要求，请参阅例程的参考页。

 

 




