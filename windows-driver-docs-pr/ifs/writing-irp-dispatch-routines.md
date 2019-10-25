---
title: 编写 IRP 调度例程
description: 编写 IRP 调度例程
ms.assetid: 8ce88932-cba6-4261-a938-d38133c20355
keywords:
- 筛选器驱动程序 WDK 文件系统、IRP 调度例程
- 文件系统筛选器驱动程序 WDK、IRP 调度例程
- 调度例程 WDK 文件系统
- IRP 调度例程 WDK 文件系统
- 编写 IRP 调度例程
- IRP 调度例程 WDK 文件系统，有关编写 IRP 调度例程
- Irp WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b3f5128c8b133858d14c514627d849dab3756d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840923"
---
# <a name="writing-irp-dispatch-routines"></a>编写 IRP 调度例程


## <span id="ddk_writing_irp_dispatch_routines_if"></span><span id="DDK_WRITING_IRP_DISPATCH_ROUTINES_IF"></span>


<div class="alert">
<strong>注意</strong>  为了获得最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>，而不是旧的文件系统筛选器驱动程序。 此外，旧文件系统筛选器驱动程序不能附加到直接访问（DAX）卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优点</a>。 若要将旧驱动程序移植到微筛选器驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">迁移旧筛选器驱动程序的准则</a>。
</div>
 

文件系统筛选器驱动程序使用类似于设备驱动程序中使用的调度例程。 *调度例程*处理一种或多种类型的 irp。 （IRP 的*类型*取决于其主要的函数代码。）驱动程序的[DriverEntry](initializing-a-file-system-filter-driver.md)例程通过将调度例程入口点存储在驱动程序对象的调度表中来*注册*这些入口点。 将 IRP 发送到驱动程序时，i/o 子系统会根据 IRP 的主要函数代码调用适当的调度例程。

每个 IRP 调度例程定义如下：

```cpp
NTSTATUS 
(*PDRIVER_DISPATCH) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp 
    ); 
```

在发起 i/o 请求的线程的上下文（通常是用户模式应用程序线程）中，文件系统筛选器驱动程序调度例程最常以 IRQL 被动\_级别进行调用。 但是，此规则有一些例外情况。 例如，页错误导致在 APC\_级别调用读写调度例程。 这些异常在[调度例程 IRQL 和线程上下文](dispatch-routine-irql-and-thread-context.md)的表中进行了总结。 遗憾的是，目前尚不能防止筛选器链中的驱动程序以 IRQL &gt; 被动\_级别（例如，无法释放旋转锁或 fast mutex）调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。 尽管如此，强烈建议筛选器调度例程始终调用**IoCallDriver** ，其调用的 IRQL 相同。

调度例程可以进行分页，前提是它们满足内核模式驱动程序体系结构设计指南的 "[进行驱动程序可分页](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-drivers-pageable)" 部分中所述的条件。

如果文件系统筛选器驱动程序具有控制设备对象（CDO），则其调度例程必须能够检测和处理 IRP 的目标设备对象是 CDO 的情况，而不是已装入卷的卷设备对象（VDO）。 有关 CDO 的详细信息，请参阅[筛选器驱动程序的控制设备对象](the-filter-driver-s-control-device-object.md)。

本部分介绍以下主题：

[完成 IRP](completing-the-irp.md)

[将 IRP 向下传递到较低级别的驱动程序](passing-the-irp-down-to-lower-level-drivers.md)

[从调度例程返回状态](returning-status-from-dispatch-routines.md)

[示例：将 IRP 向下传递而不设置完成例程](example--passing-the-irp-down-without-setting-a-completion-routine.md)

[调度例程的约束](constraints-on-dispatch-routines.md)

[调度例程 IRQL 和线程上下文](dispatch-routine-irql-and-thread-context.md)

 

 




