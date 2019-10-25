---
title: 系统工作线程
description: 系统工作线程
ms.assetid: 01ae1c1b-0cb0-4b9b-bd74-341b7c289fd4
keywords:
- executive 工作线程 WDK 内核
- 工作项 WDK 内核
- 线程对象 WDK 内核
- 项目
- WorkItemEx
- 工作线程 WDK 内核
- 工作线程回调例程 WDK 内核
- 回调例程 WDK 工作线程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ae05f02067fe6097b1cf0b95f9935b78fab2624
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838391"
---
# <a name="system-worker-threads"></a>系统工作线程





需要延迟处理的驱动程序可以使用*工作项*，其中包含指向执行实际处理的驱动程序回调例程的指针。 驱动程序将工作项排队，*系统工作线程*将从队列中删除该工作项，并运行该驱动程序的回调例程。 系统维护这些系统工作线程的池，这些线程是每次处理一个工作项的系统线程。

驱动程序[*将工作项回调例程*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_workitem_routine)与工作项关联。 当系统工作线程处理工作项时，它将调用关联的*工作*项例程。 在 Windows Vista 和更高版本的 Windows 中，驱动程序可以将[*WorkItemEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_workitem_routine_ex)例程与工作项关联起来。 *WorkItemEx*采用的参数不同于*工作*项所采用的参数。

*工作*项和*WorkItemEx*例程在系统线程上下文中运行。 如果驱动程序调度例程可以在用户模式线程上下文中运行，则该例程可以调用*工作*项或*WorkItemEx*例程来执行任何需要系统线程上下文的操作。

若要使用工作项，驱动程序需要执行以下步骤：

1.  分配并初始化新的工作项。

    系统使用[**IO\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)工作项结构来保存工作项。 若要分配新的**IO\_** 工作项结构并将其初始化为工作项，驱动程序可以调用[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)。 在 Windows Vista 和更高版本的 Windows 中，驱动程序可以或者分配其自己的**IO\_** 工作项结构，并调用[**IoInitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeworkitem)将结构初始化为一个工作项。 （驱动程序应调用[**IoSizeofWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosizeofworkitem)来确定保存工作项所需的字节数。）

2.  将回调例程与工作项关联，并将该工作项排队，以便系统工作线程可以对其进行处理。

    若要将*工作项例程与*工作项关联，并将工作项排队，驱动程序应调用[**IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)。 若要将*WorkItemEx*例程与工作项关联，并将该工作项排队，则驱动程序应调用[**IoQueueWorkItemEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitemex)。

3.  不再需要该工作项后，请将其释放。

    **IoAllocateWorkItem**分配的工作项应由[**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem)释放。 **IoInitializeWorkItem**初始化的工作项必须先由[**IoUninitializeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iouninitializeworkitem)取消初始化，然后才能释放。

    仅当工作项当前未排队时，才能取消初始化或释放工作项。 在调用工作项的回调例程之前，系统会取消排队工作项，因此可以从回调内调用**IoFreeWorkItem**和**IoUninitializeWorkItem** 。

需要启动需要漫长处理或发出阻塞调用的处理任务的 DPC 应将该任务的处理委托给一个或多个工作项。 当 DPC 运行时，将阻止所有线程运行。 此外，以 IRQL = 调度\_级别运行的 DPC 不得发出阻止调用。 不过，处理工作项的系统工作线程在 IRQL = 被动\_级别运行。 因此，工作项可以包含阻止调用。 例如，系统工作线程可以等待调度程序对象。

因为系统工作线程池是有限的资源，所以*工作*项和*WorkItemEx*例程仅可用于需要较短时间的操作。 如果其中一个例程运行的时间太长（例如，它包含一个无限循环）或等待时间太长，则系统可能会死锁。 因此，如果驱动程序需要长时间的延迟处理，则应改为调用[**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)创建自己的系统线程。

请勿调用**IoQueueWorkItem**或**IoQueueWorkItemEx**来对队列中已存在的工作项进行排队。 在选中的生成中，此错误会导致 bug 检查。 在零售版本中，不会检测到错误，但可能会导致系统数据结构损坏。 如果在每次运行特定的驱动程序例程时，驱动程序都会将同一工作项排队，则可以使用以下方法来避免第二次将工作项排队：

-   驱动程序为辅助角色维护一系列任务。
-   此任务列表在提供给 worker 例程的上下文中可用。 用于修改任务列表的辅助角色例程和任何驱动程序例程会将其访问权限同步到列表。
-   辅助角色每次运行时，都会执行列表中的所有任务，并在任务完成时从列表中删除每个任务。
-   新任务到达时，驱动程序会将此任务添加到列表。 仅当任务列表以前为空时，驱动程序才会将工作项排队。

系统工作线程会先从队列中删除工作项，然后再调用工作线程。 因此，一旦工作线程开始运行，驱动程序线程就可以安全地将工作项排队。

 

 




