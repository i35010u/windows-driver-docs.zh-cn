---
title: 使用自动同步
description: 使用自动同步
ms.assetid: be7d3c0e-c3cf-4104-ab81-5ecdcb9163c8
keywords:
- 同步 WDK KMDF
- 自动同步 WDK KMDF
- 锁定 WDK KMDF
- 设备级同步 WDK KMDF
- 队列级同步 WDK KMDF
- 无同步 WDK KMDF
- 同步作用域 WDK KMDF
- 执行级别 WDK KMDF
- WdfExecutionLevelPassive
- WdfExecutionLevelDispatch
- WdfExecutionLevelInheritFromParent
- WdfSynchronizationScopeDevice
- WdfSynchronizationScopeQueue
- WdfSynchronizationScopeNone
- WdfSynchronizationScopeInheritFromParent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3452a8b518f4523b1d23080a54d2432dc8ea648
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184573"
---
# <a name="using-automatic-synchronization"></a>使用自动同步


基于框架的驱动程序中的几乎所有代码都驻留在事件回调函数中。 框架会自动同步大多数驱动程序的回调函数，如下所示：

-   框架始终将 [常规设备](/windows-hardware/drivers/ddi/wdfdevice/#device-callbacks)对象、 [功能设备对象 (FDO) ](/windows-hardware/drivers/ddi/wdfdevice/#fdo-callbacks)和 [物理设备对象 (PDO) ](/windows-hardware/drivers/ddi/wdfdevice/#pdo-callbacks) 事件回调函数相互同步，以便每个设备一次只能调用 [*EvtDeviceSurpriseRemoval*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)、 [*EvtDeviceQueryRemove*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)和 [*EvtDeviceQueryStop*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop) 这两个回调函数 (。 这些回调函数支持即插即用 (PnP) 和电源管理事件，并在 IRQL = 被动 \_ 级别调用。

-   或者，框架可以同步处理驱动程序 i/o 请求的回调函数的执行，以便这些回调函数一次运行一个。 具体而言，框架可以将 [队列](/windows-hardware/drivers/ddi/wdfio/)、 [中断](/windows-hardware/drivers/ddi/wdfinterrupt/)、 [延迟过程调用 (DPC) ](/windows-hardware/drivers/ddi/wdfdpc/)、 [计时器](/windows-hardware/drivers/ddi/wdftimer/)、 [工作项](/windows-hardware/drivers/ddi/wdfworkitem/)和 [文件](/windows-hardware/drivers/ddi/wdffileobject/) 对象以及请求对象的 [*EvtRequestCancel*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel) 回调函数同步回调函数。 框架在 IRQL = 调度级别调用大多数这些回调函数 \_ ，但你可以强制队列和文件对象回调函数以 irql = 被动 \_ 级别运行。  (工作项回调函数始终在被动级别运行 \_ 。 ) 

框架通过使用一组内部同步锁实现此自动同步。 此框架确保两个或多个线程无法同时调用相同的回调函数，因为每个线程都必须等到它可以在调用回调函数之前获得同步锁。  (（可选），驱动程序还可以在必要时获取这些同步锁。 有关详细信息，请参阅 [使用框架锁](using-framework-locks.md)。 ) 

驱动程序应在 [对象上下文空间](framework-object-context-space.md)中存储特定于对象的数据。 如果驱动程序只使用框架定义的接口，则只有接收对象句柄的回调函数可以访问此数据。 如果框架正在同步对驱动程序的回调函数的调用，则一次只调用一个回调函数，并且每次只能对一个回调函数访问对象的上下文空间。

除非您的驱动程序实现 [被动级中断处理](supporting-passive-level-interrupts.md)，否则，服务中断和访问中断数据的代码必须在设备的 IRQL (DIRQL) 运行，并且需要额外的同步。 有关详细信息，请参阅 [同步中断代码](synchronizing-interrupt-code.md)。

如果你的驱动程序启用处理 i/o 请求的回调函数的自动同步，则框架将同步这些回调函数，以便每次运行一个。 下表列出了框架同步的回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象类型</th>
<th align="left">同步回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Queue 对象</p></td>
<td align="left"><p><a href="request-handlers.md" data-raw-source="[Request handlers](request-handlers.md)">请求处理程序</a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state" data-raw-source="[&lt;em&gt;EvtIoQueueState&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)"><em>EvtIoQueueState</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>File 对象</p></td>
<td align="left"><p>所有 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/" data-raw-source="[callback functions](/windows-hardware/drivers/ddi/wdffileobject/)">回调函数</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>请求对象</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel" data-raw-source="[&lt;em&gt;EvtRequestCancel&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)"><em>EvtRequestCancel</em></a></p></td>
</tr>
</tbody>
</table>

 

或者，框架还可以将这些回调函数与驱动程序为设备提供的任何中断、DPC、工作项和计时器对象回调函数同步， (排除中断对象的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数) 。 若要启用此附加同步，驱动程序必须将这些对象的配置结构的 **AutomaticSerialization** 成员设置为 **TRUE**。

总而言之，框架的自动同步功能提供了以下功能：

-   框架始终同步每个设备的 PnP 和电源管理回调函数。

-   或者，框架可以同步 i/o 队列的请求处理程序和一些额外的回调函数 (参阅上表) 。

-   驱动程序可以要求框架为中断、DPC、工作项和计时器对象同步回调函数。

-   驱动程序必须通过使用 [同步中断代码](synchronizing-interrupt-code.md)中所述的技术来同步服务中断和访问中断数据的代码。

-   此框架不会同步驱动程序的其他回调函数（如驱动程序的 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 回调函数）或 i/o 目标对象定义的回调函数。 相反，该框架提供其他 [锁](using-framework-locks.md) ，驱动程序可以使用这些锁来同步这些回调函数。

### <a name="choosing-a-synchronization-scope"></a>选择同步作用域

您可以选择让框架同步所有与设备的 i/o 队列相关联的回调函数。 或者，可以选择让框架分别同步设备的每个 i/o 队列的回调函数。 可用于驱动程序的同步选项如下所示：

-   设备级同步

    对于所有设备的 i/o 队列，框架将同步上一个表中包含的回调函数，以便每次运行一个。 在调用回调函数之前，框架通过获取设备的同步锁来实现此同步。

-   队列级同步

    对于每个单独的 i/o 队列，框架将同步上一个表中包含的回调函数，以便每次运行一个。 在调用回调函数之前，框架通过获取队列的同步锁来实现此同步。

-   无同步

    此框架不会同步上一个表中包含的回调函数的执行，也不会在调用回调函数之前获取同步锁。 如果需要同步，驱动程序必须提供。

若要指定框架是否为驱动程序提供设备级别的同步、队列级同步或无同步，可以为驱动程序对象、设备对象或队列对象指定 *同步作用域* 。 对象的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构的**SynchronizationScope**成员标识该对象的同步作用域。 驱动程序可以指定的同步作用域值包括：

<a href="" id="wdfsynchronizationscopedevice"></a>**WdfSynchronizationScopeDevice**  
框架通过获取设备对象的同步锁进行同步。

<a href="" id="wdfsynchronizationscopequeue"></a>**WdfSynchronizationScopeQueue**  
框架通过获取队列对象的同步锁进行同步。

<a href="" id="wdfsynchronizationscopenone"></a>**WdfSynchronizationScopeNone**  
框架不会同步，也不会获得同步锁。

<a href="" id="wdfsynchronizationscopeinheritfromparent"></a>**WdfSynchronizationScopeInheritFromParent**  
框架从对象的父对象获取对象的 **SynchronizationScope** 值。

通常，我们不建议使用设备级同步。

有关同步范围值的详细信息，请参阅 [**WDF \_ 同步 \_ 范围**](/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_synchronization_scope)。

驱动程序对象的默认同步作用域为 **WdfSynchronizationScopeNone**。 设备和队列对象的默认同步作用域为 **WdfSynchronizationScopeInheritFromParent**。

如果希望框架为所有设备提供设备级同步，可以使用以下步骤：

1.  在驱动*程序的驱动程序*对象的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构中，将**SynchronizationScope**设置为**WdfSynchronizationScopeDevice** 。

2.  为每个*设备*对象使用默认的**WdfSynchronizationScopeInheritFromParent**值。

或者，若要为单个设备提供设备级同步，可以使用以下步骤：

1.  对*driver*对象使用默认的**WdfSynchronizationScopeNone**值。

2.  在单个*设备*对象的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构中，将**SynchronizationScope**设置为**WdfSynchronizationScopeDevice** 。

如果希望框架为设备提供队列级同步，可使用以下方法：

-   对于 framework 版本1.9 及更高版本，应通过在 queue 对象的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构中设置**WdfSynchronizationScopeQueue** ，为各个队列启用队列级同步。 这是首选方法。

-   或者，你可以在所有框架版本中使用以下步骤：
    1.  在*设备*对象的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构中，将**SynchronizationScope**设置为**WdfSynchronizationScopeQueue** 。
    2.  为每个设备的*队列*对象使用默认的**WdfSynchronizationScopeInheritFromParent**值。

如果你不希望框架同步处理驱动程序的 i/o 请求的回调函数，请对驱动程序的驱动程序、设备和队列对象使用默认的 **SynchronizationScope** 值。 在这种情况下，框架不会自动同步驱动程序的与 i/o 请求相关的回调函数，并且可以在 IRQL &lt; = 调度级别调用回调函数 \_ 。

请注意，设置 **SynchronizationScope** 值仅同步上表中包含的回调函数。 如果希望框架还同步驱动程序的中断、DPC、工作项和计时器对象回调函数，驱动程序必须将这些对象的配置结构的 **AutomaticSerialization** 成员设置为 **TRUE**。

但是，仅当你想要同步的所有回调函数都在相同的 IRQL 下运行时，才可以将 **AutomaticSerialization** 设置为 **TRUE** 。 选择下面所述的 *执行级别*可能会导致不兼容的 IRQL 级别。 在这种情况下，驱动程序必须使用 [框架锁](using-framework-locks.md) ，而不是设置 **AutomaticSerialization**。 有关中断、DPC、工作项和计时器对象的配置结构的详细信息，以及有关适用于在这些结构中设置 **AutomaticSerialization** 的限制的详细信息，请参阅 [**wdf \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)、 [**wdf \_ DPC \_ config**](/windows-hardware/drivers/ddi/wdfdpc/ns-wdfdpc-_wdf_dpc_config)、 [**wdf 工作项 \_ \_ 配置**](/windows-hardware/drivers/ddi/wdfworkitem/ns-wdfworkitem-_wdf_workitem_config)和 [**wdf \_ 计时器 \_ 配置**](/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)。

如果将 **AutomaticSerialization** 设置为 **TRUE**，则应选择 "队列级同步"。

### <a name="choosing-an-execution-level"></a>选择执行级别

当驱动程序创建某些类型的框架对象时，它可以指定对象的 *执行级别* 。 执行级别指定框架将在其上调用对象的事件回调函数（用于处理驱动程序的 i/o 请求）的 IRQL。

如果驱动程序提供执行级别，则提供的级别会影响队列和文件对象的回调函数。 通常，如果驱动程序使用自动同步，则框架将调用这些回调函数的 IRQL = 调度 \_ 级别。 通过指定执行级别，驱动程序可以强制框架以 IRQL = 被动级别调用这些回调函数 \_ 。 设置将在其中调用队列和文件对象回调函数的 IRQL 时，框架使用以下规则：

-   如果驱动程序使用自动同步，则其队列和文件对象回调函数将在 IRQL = 调度 \_ 级别调用，除非该驱动程序要求框架在 IRQL = 被动级别调用其回调函数 \_ 。

-   如果驱动程序未使用自动同步并且未指定执行级别，则可在 IRQL = 调度级别调用驱动程序的队列和文件对象回调函数 &lt; \_ 。

请注意，如果您的驱动程序提供文件对象回调函数，则您很可能希望框架在 IRQL = 被动级别调用这些回调函数， \_ 因为某些文件数据（如文件名）是可分页的。

若要提供执行级别，驱动程序必须为对象的[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构的**ExecutionLevel**成员指定值。 驱动程序可以指定的执行级别值包括：

<a href="" id="wdfexecutionlevelpassive"></a>**WdfExecutionLevelPassive**  
框架在 IRQL = 被动级别调用对象的回调函数 \_ 。

<a href="" id="wdfexecutionleveldispatch"></a>**WdfExecutionLevelDispatch**  
框架可以在 IRQL = 调度级别调用对象的回调函数 &lt; \_ 。  (如果驱动程序使用自动同步，则框架始终以 IRQL = 调度级别调用回调函数 \_ 。 ) 

<a href="" id="wdfexecutionlevelinheritfromparent"></a>**WdfExecutionLevelInheritFromParent**  
框架从对象的父对象获取对象的 **ExecutionLevel** 值。

驱动程序对象的默认执行级别为 **WdfExecutionLevelDispatch**。 所有其他对象的默认执行级别为 **WdfExecutionLevelInheritFromParent**。

有关执行级别值的详细信息，请参阅 [**WDF \_ 执行 \_ 级别**](/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_execution_level)。

下表显示了在这种情况下，框架可以调用驱动程序的队列对象和文件对象的回调函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">同步范围</th>
<th align="left">执行级别</th>
<th align="left">队列和文件回调函数的 IRQL</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>WdfSynchronizationScopeDevice</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfSynchronizationScopeDevice</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelDispatch</strong></p></td>
<td align="left"><p>DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>WdfSynchronizationScopeQueue</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfSynchronizationScopeQueue</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelDispatch</strong></p></td>
<td align="left"><p>DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>WdfSynchronizationScopeNone</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfSynchronizationScopeNone</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelDispatch</strong></p></td>
<td align="left"><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

 

对于驱动程序、设备、文件、队列、计时器和常规对象，可以将执行级别设置为 **WdfExecutionLevelPassive** 或 **WdfExecutionLevelDispatch** 。 对于其他对象，只允许使用 **WdfExecutionLevelInheritFromParent** 。

应在以下情况中指定 **WdfExecutionLevelPassive** ：

-   驱动程序的回调函数必须调用 framework 方法或 Windows 驱动模型 (WDM) 例程，这些例程只能在 IRQL = 被动 \_ 级别调用。

-   驱动程序的回调函数必须访问可分页的代码或数据。  (例如，文件对象回调函数通常访问可分页的数据。 ) 

你的驱动程序可以设置**WdfExecutionLevelDispatch**并提供一个回调函数，该函数可创建[工作项](using-framework-work-items.md)，而不是设置**WdfExecutionLevelPassive**，因为它必须处理 IRQL = 被动级别的某些操作 \_ 。

在确定驱动程序是否应将对象的执行级别设置为 **WdfExecutionLevelPassive**之前，应确定驱动程序中的驱动程序和其他驱动程序调用的 IRQL。 请考虑以下情况：

-   如果你的驱动程序位于内核模式驱动程序堆栈的顶部，则系统通常会以 IRQL = 被动级别调用驱动程序 \_ 。 此类驱动程序的客户端可能是基于 UMDF 的驱动程序或用户模式应用程序。 指定 **WdfExecutionLevelPassive** 不会对驱动程序的性能产生负面影响，因为框架不需要将驱动程序的调用排队到 IRQL = 被动级别调用的工作项 \_ 。

-   如果驱动程序不在堆栈顶部，则系统可能不会以 IRQL = 被动级别调用驱动程序 \_ 。 因此，框架必须将您的驱动程序的调用排队，以便以后在 IRQL = 被动级别调用这些工作项 \_ 。 相比，此过程可能会导致驱动程序性能不佳，比较是允许在 IRQL = 调度级别调用驱动程序的回调函数 &lt; \_ 。

对于 DPC 对象和不表示[被动级别计时器](using-timers.md)的计时器对象，请注意，如果已将父设备的执行级别设置为 " **WdfExecutionLevelPassive**"，则不能将配置结构的**AutomaticSerialization**成员设置为**TRUE** 。 这是因为，框架将以 IRQL = 被动级别获取设备对象的 [回调同步锁](using-framework-locks.md) ， \_ 因此不能使用锁来同步 DPC 或计时器对象回调函数，该函数必须以 IRQL = 调度 \_ 级别执行。 在这种情况下，你的驱动程序应在必须相互同步的任何设备、DPC 或计时器对象回调函数中使用 [framework 旋转锁](using-framework-locks.md#framework-spin-locks) 。

另请注意，*对于表示被动级别计时器的计时器*对象，仅当父设备的执行级别设置为**WdfExecutionLevelPassive**时，*才*可以将配置结构的**AutomaticSerialization**成员设置为 TRUE。

 

