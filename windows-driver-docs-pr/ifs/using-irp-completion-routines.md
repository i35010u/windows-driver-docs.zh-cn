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
ms.openlocfilehash: 2a6055345cadd4753dcbc282a438a798e6a5cd2f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066098"
---
# <a name="using-irp-completion-routines"></a>使用 IRP 完成例程

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的 [文件系统微筛选器驱动程序](./filter-manager-concepts.md) ，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅 [迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

文件系统筛选器驱动程序使用与设备驱动程序使用的完成例程。 *完成例程*对 IRP 执行完成处理。 将 IRP 向下传递到下一个较低级别驱动程序的任何驱动程序例程，都可以通过在调用[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)之前调用[**IOSETCOMPLETIONROUTINE**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，为 irp 注册一个完成例程。

每个 IRP 完成例程定义如下：

```cpp
NTSTATUS
(*PIO_COMPLETION_ROUTINE) (
    IN PDEVICE_OBJECT DeviceObject,
    IN PIRP Irp,
    IN PVOID Context
    );
```

完成例程在任意线程上下文中以 IRQL <= DISPATCH_LEVEL 的情况下调用。

由于它们可以在 DISPATCH_LEVEL IRQL 的情况下调用，因此完成例程无法调用必须在较低的 IRQL （如 [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)）中调用的内核模式例程。 出于同一原因，必须从非分页池分配完成例程中使用的任何数据结构。

本部分介绍以下主题：

[如何执行完成处理](how-completion-processing-is-performed.md)

[检查 PendingReturned 标志](checking-the-pendingreturned-flag.md)

[从完成例程返回状态](returning-status-from-completion-routines.md)

[示例：简单的传递调度和完成](example--simple-pass-through-dispatch-and-completion.md)

[完成例程的约束](constraints-on-completion-routines.md)