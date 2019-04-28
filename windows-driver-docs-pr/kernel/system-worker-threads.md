---
title: 系统工作线程
description: 系统工作线程
ms.assetid: 01ae1c1b-0cb0-4b9b-bd74-341b7c289fd4
keywords:
- executive 辅助线程 WDK 内核
- 工作项 WDK 内核
- 线程对象 WDK 内核
- WorkItem
- WorkItemEx
- 辅助角色线程 WDK 内核
- 工作线程回调例程 WDK 内核
- 回调例程 WDK 工作线程数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf3ce35dd4cafaa2cc890874199c6ceb77323031
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345405"
---
# <a name="system-worker-threads"></a>系统工作线程





可以使用的驱动程序，需要延迟的处理*工作项*，其中包含指向执行实际处理的驱动程序回调例程的指针。 该驱动程序队列工作项和一个*系统工作线程*从队列中移除工作项和运行驱动程序的回调例程。 系统会维护这些系统工作线程，每一次处理一个工作项的系统线程池。

驱动程序相关联[*工作项*](https://msdn.microsoft.com/library/windows/hardware/ff566380)与工作项的回调例程。 当系统工作线程处理的工作项时，它将调用相关联*工作项*例程。 在 Windows Vista 和更高版本的 Windows 中，驱动程序可以改为将相关联[ *WorkItemEx* ](https://msdn.microsoft.com/library/windows/hardware/ff566381)例程与工作项。 *WorkItemEx*采用不同于参数的参数的*工作项*采用。

*工作项*并*WorkItemEx*例程在系统线程上下文中运行。 如果驱动程序调度例程可以在用户模式线程上下文中运行，可以调用该例程*工作项*或*WorkItemEx*例程，以执行需要系统线程上下文的任何操作。

若要使用工作项，驱动程序，请执行以下步骤：

1.  分配并初始化新的工作项。

    系统将使用[ **IO\_工作项**](https://msdn.microsoft.com/library/windows/hardware/ff550679)结构，用于保存工作项。 若要分配一个新**IO\_工作项**结构，并将其初始化为工作项，驱动程序可以调用[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)。 在 Windows Vista 和更高版本的 Windows 中，该驱动程序可以或者分配其自己**IO\_工作项**结构，并调用[ **IoInitializeWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549349)初始化为工作项结构。 (该驱动程序应调用[ **IoSizeofWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff550352)来确定所需保存工作项的字节数。)

2.  工作项相关联的回调例程和队列工作项，以便它将由系统工作线程处理。

    若要将相关联*工作项*例程与工作项和队列工作项，该驱动程序应调用[ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)。 若要改为将相关联*WorkItemEx*例程与工作项和队列工作项，该驱动程序应调用[ **IoQueueWorkItemEx**](https://msdn.microsoft.com/library/windows/hardware/ff549474)。

3.  不再需要工作项后，释放它。

    由分配的工作项**IoAllocateWorkItem**应释放[ **IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)。 已初始化的工作项**IoInitializeWorkItem**必须通过未初始化[ **IoUninitializeWorkItem** ](https://msdn.microsoft.com/library/windows/hardware/ff550392)可释放之前。

    只能未初始化或释放当前未排队的工作项时工作项。 系统通过工作项取消排队，因此调用工作项的回调例程之前**IoFreeWorkItem**并**IoUninitializeWorkItem**可以从在回调过程中调用。

需要启动处理任务的需要长时间的处理或执行阻止调用 DPC 应委托给一个或多个工作项任务的处理。 DPC 时，所有线程不都能运行。 此外，DPC 它运行在 IRQL = 调度\_级别，不得阻止调用。 但是，在处理工作项的系统工作线程运行在 IRQL = 被动\_级别。 因此，工作项可以包含阻止调用。 例如，系统工作线程可以等待调度程序对象。

系统工作线程池是一种有限的资源，因为*工作项*并*WorkItemEx*例程可以仅用于需要短时间内的操作。 如果每个例程运行太长时间 （如果它包含一个无限循环，例如） 或等待太长，系统会出现死锁。 因此，如果驱动程序需要很长一段延迟处理，则应改为调用[ **PsCreateSystemThread** ](https://msdn.microsoft.com/library/windows/hardware/ff559932)创建其自己的系统线程。

不要调用**IoQueueWorkItem**或**IoQueueWorkItemEx**若要在队列中已将工作项排队。 在已检查生成此错误会导致的 bug 检查。 在零售版本中，该错误未检测到，但可能会导致系统损坏的数据结构。 如果您的驱动程序队列相同的工作项每次运行的特定驱动程序例程，您可以使用以下技术来避免队列工作项第二次，如果已在队列中：

-   该驱动程序维护的任务的工作线程例程的列表。
-   提供给工作线程例程的上下文中提供了此任务列表。 辅助角色例程，并修改任务列表的任何驱动程序例程同步其访问列表的权限。
-   每次工作人员日常运行时，它在列表中，将执行所有任务并从列表中删除每个任务，为该任务已完成。
-   当新任务到达时，该驱动程序将此任务添加到列表。 驱动程序队列工作项，仅当任务列表是先前为空。

调用工作线程之前系统工作线程从队列中移除工作项。 因此，驱动程序线程可以安全地工作项排队以再次立即工作线程开始运行。

 

 




