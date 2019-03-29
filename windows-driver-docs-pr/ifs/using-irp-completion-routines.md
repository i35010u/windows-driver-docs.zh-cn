---
title: 使用 IRP 完成例程
description: 使用 IRP 完成例程
ms.assetid: 82b9ba2b-17db-40e5-be3f-fd77cd986781
keywords:
- 筛选器驱动程序 WDK 文件系统，IRP 完成例程
- 文件系统筛选器驱动程序 WDK、 IRP 完成例程
- IRP 完成例程 WDK 文件系统
- Irp WDK 文件系统
- 完成 I/O 请求 WDK 文件系统
- IRP 完成例程 WDK 文件系统，有关 IRP 完成例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338c545fd61f462936207280f66cf8504b53f1b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563053"
---
# <a name="using-irp-completion-routines"></a>使用 IRP 完成例程


## <span id="ddk_using_irp_completion_routines_if"></span><span id="DDK_USING_IRP_COMPLETION_ROUTINES_IF"></span>


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

文件系统筛选器驱动程序使用类似于所使用的设备驱动程序的完成例程。 一个*完成例程*执行完成处理 IRP。 将传递到下一步低级驱动程序 IRP 的任何驱动程序例程可以选择注册完成例程的 IRP 通过调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)之前调用[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。

每个 IRP 完成例程定义，如下所示：

```cpp
NTSTATUS 
(*PIO_COMPLETION_ROUTINE) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp, 
    IN PVOID Context 
    ); 
```

IRQL 在调用完成例程&lt;= 调度\_级别，请在任意线程上下文中。

因为在 IRQL 调度调用它们\_级别，完成例程不能调用必须在较低的 IRQL，如调用的内核模式例程[ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)。 出于相同原因，必须从非分页缓冲池分配完成例程中使用任何数据结构。

本部分讨论以下主题：

[完成处理的执行方式](how-completion-processing-is-performed.md)

[检查 PendingReturned 标志](checking-the-pendingreturned-flag.md)

[从完成例程返回状态](returning-status-from-completion-routines.md)

[示例：简单传递调度和完成](example--simple-pass-through-dispatch-and-completion.md)

[完成例程的约束](constraints-on-completion-routines.md)

 

 




