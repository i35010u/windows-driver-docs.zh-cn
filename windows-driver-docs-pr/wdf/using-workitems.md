---
title: 使用工作项
description: 使用工作项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 267f49f2e50b5511a84652ed7d1bf98ce97edda5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821097"
---
# <a name="using-work-items"></a>使用工作项


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

工作项是驱动程序在 [*OnWorkItem*](/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function) 事件回调函数中执行的任务。 这些函数以异步方式运行。

如果 [*OnInterruptIsr*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr) 必须在不延迟 (ISR 的中断服务请求的执行的情况下执行额外的处理，则 UMDF 驱动程序通常使用工作项) 因为中断线路可能由多个设备共享。

通常，驱动程序的 [*OnInterruptIsr*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr) 回调函数将创建工作项对象，并将其添加到系统的工作项队列中。 然后，threadpool 线程取消排队对象并调用工作项的 [*OnWorkItem*](/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function) 回调函数。

## <a name="setting-up-a-work-item"></a>设置工作项


若要设置工作项，驱动程序必须：

1.  创建工作项。

    驱动程序调用 [**IWDFDevice3：： CreateWorkItem**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem) 来创建工作项对象，并标识将处理该工作项的 [*OnWorkItem*](/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function) 回调函数。

2.  存储有关工作项的信息。

    通常，驱动程序使用工作项对象的上下文内存来存储有关 [*OnWorkItem*](/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function) 回调函数应执行的任务的信息。 调用 *OnWorkItem* 回调函数时，它可以通过访问此上下文内存来检索信息。 有关如何分配和访问上下文内存的信息，请参阅 [**IWDFObject：： AssignContext**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)。

3.  将工作项添加到系统的工作项队列中。

    你的驱动程序将调用 [**IWDFWorkItem：：排队**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-enqueue)，这会将驱动程序的工作项添加到工作项队列。

当驱动程序调用 [**IWDFDevice3：： CreateWorkItem**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)时，它可能会根据需要提供父对象 (例如设备对象或) 的队列对象。 当系统删除该对象时，它还会删除与该对象关联的任何现有工作项。

## <a name="using-the-workitem-callback-function"></a>使用工作项回调函数


在将工作项添加到工作项队列后，它将保留在队列中，直到系统工作线程变为可用。 系统工作线程将从队列中删除工作项，然后调用驱动程序的 OnWorkItem 回调函数，并将工作项对象作为输入传递。

通常，OnWorkItem 回调函数执行以下步骤：

1.  通过访问工作项对象的上下文内存获取有关工作项的驱动程序提供的信息。
2.  执行指定的任务。 如有必要，回调函数可以调用 [**IWDFWorkItem：： GetParentObject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-getparentobject) 来确定工作项的父对象。
3.  如果驱动程序将重新排队工作项，则指示工作项的句柄现在可用于重用。

几个驱动程序可能需要调用 [**IWDFWorkItem：： flush**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-flush) 来刷新工作项队列中的工作项。 如果驱动程序调用了 **Flush** 方法，则该方法不会返回，直到工作线程已从工作项队列中删除指定的工作项，并调用了驱动程序的 [*OnWorkItem*](/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function) 回调函数，并且 *OnWorkItem* 回调函数随后在处理工作项后返回。

 

