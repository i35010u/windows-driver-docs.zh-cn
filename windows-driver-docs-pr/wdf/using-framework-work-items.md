---
title: 使用框架工作项
description: 使用框架工作项
keywords:
- 工作项 WDK KMDF
- 队列 WDK KMDF，框架工作项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac701ca5bbd48b8a6b75dc72a9bd8941d433f922
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838703"
---
# <a name="using-framework-work-items"></a>使用框架工作项





*工作项* 是驱动程序在 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)事件回调函数中执行的任务。 \_在系统工作线程的上下文中，这些函数在 IRQL = 被动级别上以异步方式运行。

基于框架的驱动程序通常使用工作项（如果 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EVTDPCFUNC*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 函数以 irql = 调度级别运行 \_ ），则必须在 irql = 被动级别执行额外的处理 \_ 。

换句话说，如果运行于 IRQL = 调度级别的函数 \_ 必须调用只能在 irql = 被动级别调用的函数，则驱动程序可以使用工作项 \_ 。

通常，驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 回调函数会创建一个工作项对象，并将其添加到系统的工作项队列中。 然后，系统工作线程取消排队对象并调用工作项的 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数。

### <a name="sample-drivers-that-use-work-items"></a>使用工作项的示例驱动程序

使用工作项的[基于框架的示例驱动程序](sample-kmdf-drivers.md)包括1394、AMCC5933、PCIDRV 和 Toaster。

### <a name="setting-up-a-work-item"></a><a href="" id="ddk-setting-up-a-work-item-df"></a>设置工作项

若要设置工作项，驱动程序必须：

1.  创建工作项。

    驱动程序调用 [**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate) 来创建工作项对象，并标识将处理该工作项的 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数。

2.  存储有关工作项的信息。

    通常，驱动程序使用工作项对象的上下文内存来存储有关 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数应执行的任务的信息。 调用 *EvtWorkItem* 回调函数时，它可以通过访问此上下文内存来检索信息。 有关如何分配和访问上下文内存的信息，请参阅 [框架对象上下文空间](framework-object-context-space.md)。

3.  将工作项添加到系统的工作项队列中。

    驱动程序调用 [**WdfWorkItemEnqueue**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，这会将驱动程序的工作项添加到工作项队列。

当驱动程序调用 [**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)时，它必须提供框架设备对象或框架队列对象的句柄。 当系统删除该对象时，它还会删除与该对象关联的任何现有工作项。 将释放工作项对象，并在调用父对象的 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 回调之前清除其关联的工作项回调。

有关框架对象层次结构的清理规则的详细信息，请参阅 [框架对象生命周期](./framework-object-life-cycle.md)。

### <a name="using-the-work-item-callback-function"></a><a href="" id="ddk-using-the-work-item-callback-function-df"></a>使用 Work-Item 回调函数

在将工作项添加到工作项队列后，它将保留在队列中，直到系统工作线程变为可用。 系统工作线程将从队列中删除工作项，然后调用驱动程序的 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数，并将工作项对象作为输入传递。

通常， [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数执行以下步骤：

1.  通过访问工作项对象的上下文内存获取有关工作项的驱动程序提供的信息。

2.  执行指定的任务。 如有必要，回调函数可以调用 [**WdfWorkItemGetParentObject**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemgetparentobject) 来确定工作项的父对象。

3.  调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，以删除工作项对象; 或者，如果驱动程序将重新排队工作项，则指示工作项的句柄现在可重复使用。

每个工作项的回调函数执行的任务必须相对较短。 操作系统提供有限数量的系统工作线程，因此，如果您的驱动程序使用工作项回调函数来执行耗时的任务，则您的驱动程序会影响系统性能。

### <a name="creating-and-deleting-work-items"></a><a href="" id="ddk-creating-and-deleting-work-items-df"></a>创建和删除工作项

驱动程序可以使用以下两种方法之一来创建和删除工作项：

-   每个工作项一次：在需要时创建工作项，并在使用后立即将其删除。

    此方法对于需要少量工作项的每) 分钟 (不频繁地使用的驱动程序很有用。

    例如，驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数可以调用 [**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate) ，然后调用 [**WdfWorkItemEnqueue**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，工作项的 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数可以调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。

    如果你的驱动程序遵循这种情况，并且其 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数接收到的状态 \_ \_ 资源不足，无法从 [**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)中返回值，则驱动程序必须能够推迟所需的工作，直到系统资源 (通常) 可用。

-   根据需要创建一个或多个驱动程序会的工作项。

    此方法对于以下情况非常有用：使用工作项的驱动程序经常 (每分钟) 或驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数无法轻松地处理 \_ \_ [**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)的资源返回值。

    在驱动程序调用 [**WdfWorkItemEnqueue**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)之前，系统不会将工作线程分配给工作项。 因此，尽管系统工作线程是有限的资源，但在初始化设备时创建工作项会消耗少量的内存，但不会影响系统性能。

    以下步骤描述了可能的方案：

    1.  驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数调用 [**WdfWorkItemCreate**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate) 来获取工作项句柄。
    2.  驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数使用步骤1中的句柄创建 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数必须执行的操作的列表，然后调用 [**WdfWorkItemEnqueue**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)。
    3.  驱动程序的 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数执行操作列表，并设置标志以指示回调函数已运行。

    接下来，每次调用驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数时，它必须确定 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数是否已运行。 如果 *EvtWorkItem* 回调函数尚未运行， *EvtInterruptDpc* 回调函数将不会调用 [**WdfWorkItemEnqueue**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，因为工作项仍处于排队。 在这种情况下， *EvtInterruptDpc* 回调函数仅更新 *EvtWorkItem* 回调函数的操作列表。

    每个工作项都与设备或队列关联。 删除关联的设备或队列后，框架会删除所有关联的工作项，因此，如果使用此方法，则驱动程序不必调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。

几个驱动程序可能需要调用 [**WdfWorkItemFlush**](/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemflush) 以从工作项队列中刷新其工作项。 有关使用 **WdfWorkItemFlush** 的示例，请参阅该方法的参考页。

如果驱动程序在未完成的工作项上调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，则结果取决于工作项的状态：

|工作项状态|结果|
|-|-|
|已创建但未排队|立即清理工作项。|
|已排队|对 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 的调用将等待，直到工作项完成执行，然后清理工作项|
|执行|如果驱动程序从同一线程) 上的 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) (中调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，则 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)将立即返回。 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)完成后，将清理工作项。  否则， [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 将等待 EvtWorkItem 完成。|

