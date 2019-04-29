---
title: 编写 IRP 调度例程
description: 编写 IRP 调度例程
ms.assetid: 8ce88932-cba6-4261-a938-d38133c20355
keywords:
- 筛选器驱动程序 WDK 文件系统，IRP 调度例程
- 文件系统筛选器驱动程序 WDK，IRP 调度例程
- 调度例程 WDK 文件系统
- IRP 调度例程 WDK 文件系统
- 编写 IRP 调度例程
- IRP 调度例程 WDK 文件系统中，有关编写 IRP 调度例程
- Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff91cc55e650034135110bf976f808f6cffae1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367154"
---
# <a name="writing-irp-dispatch-routines"></a>编写 IRP 调度例程


## <span id="ddk_writing_irp_dispatch_routines_if"></span><span id="DDK_WRITING_IRP_DISPATCH_ROUTINES_IF"></span>


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

文件系统筛选器驱动程序使用类似于在设备驱动程序中使用的调度例程。 一个*调度例程*处理 Irp 的一个或多个类型。 (*类型*IRP 的由其主要函数代码。)在驱动程序[DriverEntry](initializing-a-file-system-filter-driver.md)例程*注册*调度例程的入口点存储在驱动程序对象的调度表中。 IRP 发送到驱动程序后，I/O 子系统调用适当的调度例程根据 IRP 的主要函数代码。

每个 IRP 调度例程定义，如下所示：

```cpp
NTSTATUS 
(*PDRIVER_DISPATCH) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp 
    ); 
```

文件系统筛选器驱动程序调度例程通常在 IRQL 被动调用\_级别，请在发起 I/O 请求，这通常是用户模式应用程序线程的线程上下文中。 但是，有一些例外情况，此规则。 例如，页面错误导致读取和写入 IRQL APC 时要调用的调度例程\_级别。 中的表中总结了这些异常[调度例程 IRQL 和线程上下文](dispatch-routine-irql-and-thread-context.md)。 遗憾的是，它不是当前无法阻止筛选器链中的驱动程序调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)在 IRQL&gt;被动\_级别 （例如，通过故障到释放自旋锁或快速互斥体）。 不过，强烈建议例程始终调用该筛选器调度**IoCallDriver**在相同的 IRQL 在其中调用它们。

调度例程可为可分页，假设它们符合中所述的标准[使驱动程序可分页](https://msdn.microsoft.com/library/windows/hardware/ff554346)内核模式驱动程序体系结构设计指南的部分。

如果文件系统筛选器驱动程序将控制设备对象 (CDO)，其调度例程必须能够检测和处理 IRP 的目标设备对象的 CDO 而不是已装入的卷的卷设备对象 (VDO) 情况。 有关 CDO 详细信息，请参阅[筛选器驱动程序的控制设备对象](the-filter-driver-s-control-device-object.md)。

本部分讨论以下主题：

[完成 IRP](completing-the-irp.md)

[传递到较低级别的驱动程序 IRP](passing-the-irp-down-to-lower-level-drivers.md)

[从调度例程返回状态](returning-status-from-dispatch-routines.md)

[示例：向下传递 IRP，而无需设置完成例程](example--passing-the-irp-down-without-setting-a-completion-routine.md)

[调度例程的约束](constraints-on-dispatch-routines.md)

[调度例程 IRQL 和线程上下文](dispatch-routine-irql-and-thread-context.md)

 

 




