---
title: 使用 IRP 完成例程
description: 使用 IRP 完成例程
ms.assetid: 82b9ba2b-17db-40e5-be3f-fd77cd986781
keywords:
- 筛选器驱动程序 WDK 文件系统、IRP 完成例程
- 文件系统筛选器驱动程序 WDK、IRP 完成例程
- IRP 完成例程 WDK 文件系统
- Irp WDK 文件系统
- 完成 i/o 请求 WDK 文件系统
- IRP 完成例程 WDK 文件系统，关于 IRP 完成例程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61e2acf0ae6f308b74251c6ad48d76929860f390
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840936"
---
# <a name="using-irp-completion-routines"></a>使用 IRP 完成例程


## <span id="ddk_using_irp_completion_routines_if"></span><span id="DDK_USING_IRP_COMPLETION_ROUTINES_IF"></span>


<div class="alert">
<strong>注意</strong>  为了获得最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>，而不是旧的文件系统筛选器驱动程序。 此外，旧文件系统筛选器驱动程序不能附加到直接访问（DAX）卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优点</a>。 若要将旧驱动程序移植到微筛选器驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">迁移旧筛选器驱动程序的准则</a>。
</div>
 

文件系统筛选器驱动程序使用与设备驱动程序使用的完成例程。 *完成例程*对 IRP 执行完成处理。 将 IRP 向下传递到下一个较低级别驱动程序的任何驱动程序例程，都可以通过在调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)之前调用[**IOSETCOMPLETIONROUTINE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，为 irp 注册一个完成例程。

每个 IRP 完成例程定义如下：

```cpp
NTSTATUS 
(*PIO_COMPLETION_ROUTINE) ( 
    IN PDEVICE_OBJECT DeviceObject, 
    IN PIRP Irp, 
    IN PVOID Context 
    ); 
```

完成例程在任意线程上下文中以 IRQL &lt;= 调度\_级别调用。

由于可以在 IRQL 调度\_级别调用它们，因此完成例程无法调用必须以较低的 IRQL （如[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)）调用的内核模式例程。 出于同一原因，必须从非分页池分配完成例程中使用的任何数据结构。

本部分介绍以下主题：

[如何执行完成处理](how-completion-processing-is-performed.md)

[检查 PendingReturned 标志](checking-the-pendingreturned-flag.md)

[从完成例程返回状态](returning-status-from-completion-routines.md)

[示例：简单的传递调度和完成](example--simple-pass-through-dispatch-and-completion.md)

[完成例程的约束](constraints-on-completion-routines.md)

 

 




