---
title: 使用自动同步
description: 使用自动同步
ms.assetid: be7d3c0e-c3cf-4104-ab81-5ecdcb9163c8
keywords:
- 同步 WDK KMDF
- 自动同步 WDK KMDF
- 锁定 WDK KMDF
- 设备级别同步 WDK KMDF
- 队列级别同步 WDK KMDF
- WDK KMDF 不同步
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
ms.openlocfilehash: e74574b2b899ce051eb80aa22a6c62809f1b514e
ms.sourcegitcommit: d028d25310ce028a3935bebf564d8092716903d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2019
ms.locfileid: "57254294"
---
# <a name="using-automatic-synchronization"></a>使用自动同步


几乎所有基于 framework 的驱动程序中的代码位于事件回调函数。 该框架会自动同步大多数驱动程序的回调函数，如下所示：

-   框架始终同步[常规设备对象](https://msdn.microsoft.com/library/windows/hardware/dn265631#device-callbacks)，[功能的设备对象 (FDO)](https://msdn.microsoft.com/library/windows/hardware/dn265631#fdo-callbacks)，并[物理设备对象 (PDO)](https://msdn.microsoft.com/library/windows/hardware/dn265631#pdo-callbacks)与每个事件的回调函数其他因此只需一个回调函数 (除[ *EvtDeviceSurpriseRemoval*](https://msdn.microsoft.com/library/windows/hardware/ff540913)， [ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)，并[ *EvtDeviceQueryStop*](https://msdn.microsoft.com/library/windows/hardware/ff540885)) 可以在每个设备的时间调用。 这些回调函数支持插即用 (PnP) 和电源管理事件和调用在 IRQL = 被动\_级别。

-   （可选） 该框架可以同步处理驱动程序的 I/O 请求的回调函数的执行，以便这些回调函数运行一次一个。 具体而言，框架可以同步的回调函数[队列](https://msdn.microsoft.com/library/windows/hardware/dn265647)，[中断](https://msdn.microsoft.com/library/windows/hardware/dn265640)，[延迟过程调用 (DPC)](https://msdn.microsoft.com/library/windows/hardware/dn265635)，[计时器](https://msdn.microsoft.com/library/windows/hardware/dn265670)，[工作项](https://msdn.microsoft.com/library/windows/hardware/dn265673)，并[文件](https://msdn.microsoft.com/library/windows/hardware/dn265638)对象，以及请求对象[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)回调函数。 大多数框架将调用这些回调函数在 IRQL = 调度\_级别，但您可以强制队列和文件对象回调函数来运行在 IRQL = 被动\_级别。 (工作项回调函数始终运行在被动\_级别。)

框架使用一组内部同步锁来实现此自动同步。 框架将确保两个或多个线程不能相同的回调函数调用在同一时间，因为每个线程必须等待，直到它可以调用的回调函数之前获取同步锁。 （（可选） 驱动程序还可以获取在必要时这些同步锁。 有关详细信息，请参阅[使用 Framework 锁定](using-framework-locks.md)。)

您的驱动程序应将中的特定于对象的数据存储[对象上下文空间](framework-object-context-space.md)。 如果您的驱动程序只使用框架定义接口，仅接收对象的句柄的回调函数可以访问此数据。 如果框架进行同步时对驱动程序的回调函数的调用，只能将一个回调函数将调用一次，并将一次只能将一个回调函数可访问对象的上下文空间。

除非您的驱动程序实现[被动级别中断处理](supporting-passive-level-interrupts.md)，该服务中断的代码和访问中断数据必须运行在设备的 IRQL (DIRQL) 并需要附加的同步。 有关详细信息，请参阅[同步中断代码](synchronizing-interrupt-code.md)。

如果您的驱动程序使处理 I/O 请求的回调函数的自动同步，框架将在以便一次一个地运行这些同步这些回调函数。 下表列出了同步框架的回调函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象类型</th>
<th align="left">已同步的回调函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>队列对象</p></td>
<td align="left"><p><a href="request-handlers.md" data-raw-source="[Request handlers](request-handlers.md)">请求处理程序</a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff541771" data-raw-source="[&lt;em&gt;EvtIoQueueState&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541771)"> <em>EvtIoQueueState</em></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff541779" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541779)"> <em>EvtIoResume</em></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"> <em>EvtIoStop</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>文件对象</p></td>
<td align="left"><p>所有<a href="https://msdn.microsoft.com/library/windows/hardware/dn265638" data-raw-source="[callback functions](https://msdn.microsoft.com/library/windows/hardware/dn265638)">回调函数</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>请求对象</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541817" data-raw-source="[&lt;em&gt;EvtRequestCancel&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541817)"><em>EvtRequestCancel</em></a></p></td>
</tr>
</tbody>
</table>

 

（可选） 该框架还可以同步这些与任何中断、 DPC，工作项，回调函数和计时器对象回叫函数，您的驱动程序提供设备的 (不包括中断对象[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数)。 若要启用此附加的同步，该驱动程序必须设置**AutomaticSerialization**这些对象的配置结构的成员**TRUE**。

总之，框架的自动同步功能提供了以下功能：

-   框架始终同步每个设备的即插即用和电源管理回调函数。

-   （可选） 该框架可以同步 I/O 队列的请求处理程序和一些其他回调函数 （请参阅上表）。

-   驱动程序可以让 framework 同步中断、 DPC，回调函数的工作项和计时器对象。

-   驱动程序必须同步服务中断的代码和访问中断数据通过使用中所述的技术[同步中断代码](synchronizing-interrupt-code.md)。

-   框架不会同步驱动程序的其他回调函数，如驱动程序的[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数或 I/O 目标对象定义的回调函数。 相反，该框架提供了其他[锁](using-framework-locks.md)驱动程序可用于同步这些回调函数。

### <a name="choosing-a-synchronization-scope"></a>选择同步的作用域

您可以选择让同步与所有设备的 I/O 队列都相关联的回调函数的所有框架。 或者，您可以选择让框架单独为每个设备的 I/O 队列同步回调函数。 可供您的驱动程序的同步选项如下所示：

-   设备级别同步

    该框架，以便一次一个地运行这些同步对于所有设备的 I/O 队列上的表都包含的回调函数。 该框架通过调用回调函数之前获取设备的同步锁来实现此同步。

-   队列级别同步

    该框架，以便一次一个地运行这些同步包含上一个表，为每个 I/O 队列，回调函数。 该框架通过调用回调函数之前获取队列的同步锁来实现此同步。

-   没有同步

    框架不会同步执行的上一个表包含和不会调用回调函数之前获取同步锁的回调函数。 如果需要同步，该驱动程序必须提供它。

若要指定是否希望该框架可以提供设备级别同步、 队列级别同步或您的驱动程序不同步，可以指定*同步作用域*驱动程序对象，设备对象或队列对象。 **SynchronizationScope**的对象的成员[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构标识的对象同步作用域。 可以指定您的驱动程序的同步作用域值包括：

<a href="" id="wdfsynchronizationscopedevice"></a>**WdfSynchronizationScopeDevice**  
该框架将通过获取设备对象的同步锁进行同步。

<a href="" id="wdfsynchronizationscopequeue"></a>**WdfSynchronizationScopeQueue**  
该框架将通过获取队列对象的同步锁进行同步。

<a href="" id="wdfsynchronizationscopenone"></a>**WdfSynchronizationScopeNone**  
框架不会同步，并不会获取同步锁。

<a href="" id="wdfsynchronizationscopeinheritfromparent"></a>**WdfSynchronizationScopeInheritFromParent**  
框架获取对象的**SynchronizationScope**从对象的父对象的值。

一般情况下，我们不建议使用设备级别同步。

有关同步作用域值的详细信息，请参阅[ **WDF\_同步\_范围**](https://msdn.microsoft.com/library/windows/hardware/ff552518)。

驱动程序对象的默认同步作用域**WdfSynchronizationScopeNone**。 设备和队列对象的默认同步作用域**WdfSynchronizationScopeInheritFromParent**。

如果您想让框架提供的所有设备的设备级别同步，可以使用以下步骤：

1.  设置**SynchronizationScope**到**WdfSynchronizationScopeDevice**中[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)驱动程序的结构*驱动程序*对象。

2.  使用默认**WdfSynchronizationScopeInheritFromParent**值为每个*设备*对象。

或者，若要提供各个设备的设备级别同步，可以使用以下步骤：

1.  使用默认**WdfSynchronizationScopeNone**值*驱动程序*对象。

2.  设置**SynchronizationScope**到**WdfSynchronizationScopeDevice**中[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构的各个*设备*对象。

如果您想让框架提供队列级别同步设备，提供了以下技术：

-   对于 1.9 及更高版本的 framework 版本，应通过设置启用单个队列的队列级别同步**WdfSynchronizationScopeQueue**中[ **WDF\_对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)队列对象的结构。 这是首选的技术。

-   或者，您可以在所有框架版本中使用以下步骤：
    1.  设置**SynchronizationScope**到**WdfSynchronizationScopeQueue**中[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)的结构*设备*对象。
    2.  使用默认**WdfSynchronizationScopeInheritFromParent**值为每个设备*队列*对象。

如果不希望同步处理您的驱动程序的 I/O 请求的回调函数的框架，使用默认**SynchronizationScope**驱动程序的驱动程序、 设备和队列对象的值。 在这种情况下，该框架不会自动同步，驱动程序的 I/O 请求相关的回调函数，并可以在 IRQL 调用回调函数&lt;= 调度\_级别。

请注意，设置**SynchronizationScope**值同步上一个表包含的回调函数。 如果想让框架还将同步的驱动程序中断、 DPC，工作项，并且必须设置计时器对象回调函数，该驱动程序**AutomaticSerialization** 这些对象的配置结构的成员**TRUE**。

但是，可以设置**AutomaticSerialization**到**TRUE**仅当你想要同步的回调函数的所有运行在相同的 IRQL。 选择*执行级别*，接下来，对此进行描述可能会导致不兼容的 IRQL 级别。 在这种情况下，该驱动程序必须使用[framework 锁](using-framework-locks.md)而不是设置**AutomaticSerialization**。 详细了解中断、 DPC，配置结构工作项和计时器对象和限制适用于设置的详细信息**AutomaticSerialization**在这些结构中，请参阅[**WDF\_中断\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff552347)， [ **WDF\_DPC\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551296)， [ **WDF\_工作项\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff553086)，和[ **WDF\_计时器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552519).

如果您设置**AutomaticSerialization**到**TRUE**，应选择队列级别同步。

### <a name="choosing-an-execution-level"></a>选择执行级别

当驱动程序创建某些类型的 framework 对象时，它可以指定*执行级别*对象。 执行级别指定的框架将调用对象的事件处理驱动程序的 I/O 请求的回调函数 IRQL。

如果驱动程序提供的执行级别，请提供的级别会影响队列和文件对象的回调函数。 通常，如果该驱动程序使用自动同步，框架将调用这些回调函数在 IRQL = 调度\_级别。 通过指定执行级别，该驱动程序可以强制框架在调用这些回调函数调用在 IRQL = 被动\_级别。 设置 IRQL 在哪个队列和文件调用对象的回调函数时，框架将使用以下规则：

-   如果驱动程序将使用自动同步功能，其队列和文件对象回调函数调用在 IRQL = 调度\_级别，除非该驱动程序要求框架在调用其回调函数调用在 IRQL = 被动\_级别。

-   如果驱动程序不使用自动同步，且未指定的执行级别，驱动程序的队列和文件对象回调函数可以调用在 IRQL &lt;= 调度\_级别。

请注意，如果您的驱动程序提供文件对象的回调函数，您将很可能需要框架在调用这些回调函数调用在 IRQL = 被动\_级别因为某些文件数据，例如文件名称，是可分页。

若要提供的执行级别，您的驱动程序必须指定的值**ExecutionLevel**的对象的成员[ **WDF\_对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)结构。 可以指定您的驱动程序的执行级别值包括：

<a href="" id="wdfexecutionlevelpassive"></a>**WdfExecutionLevelPassive**  
框架将调用该对象的回调功能在 IRQL = 被动\_级别。

<a href="" id="wdfexecutionleveldispatch"></a>**WdfExecutionLevelDispatch**  
框架在 IRQL 就可以调用该对象的回调功能&lt;= 调度\_级别。 (如果该驱动程序使用自动同步，framework 始终调用回调函数在 IRQL = 调度\_级别。)

<a href="" id="wdfexecutionlevelinheritfromparent"></a>**WdfExecutionLevelInheritFromParent**  
框架获取对象的**ExecutionLevel**从对象的父对象的值。

驱动程序对象的默认执行级别**WdfExecutionLevelDispatch**。 所有其他对象的默认执行级别**WdfExecutionLevelInheritFromParent**。

有关执行级别值的详细信息，请参阅[ **WDF\_执行\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff551310)。

下表显示的 framework 可以为队列对象和文件对象调用驱动程序的回调函数的 IRQL 级别。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">同步作用域</th>
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

 

您可以执行级别设置为**WdfExecutionLevelPassive**或**WdfExecutionLevelDispatch**驱动程序、 设备、 文件、 队列、 计时器和一般的对象。 对于其他对象，仅**WdfExecutionLevelInheritFromParent**允许。

应指定**WdfExecutionLevelPassive**如果：

-   驱动程序的回调函数都必须调用框架方法或 Windows 驱动程序模型 (WDM) 例程可以调用仅在 IRQL = 被动\_级别。

-   驱动程序的回调函数必须访问的可分页的代码或数据。 （例如，文件对象回调函数通常访问可分页的数据。）

而不是设置**WdfExecutionLevelPassive**，可以设置您的驱动程序**WdfExecutionLevelDispatch** ，并提供一个回调函数来创建[工作项](using-framework-work-items.md)如果它必须处理某些操作在 IRQL = 被动\_级别。

在决定是否您的驱动程序应对象的执行级别设置为之前**WdfExecutionLevelPassive**，应确定您的驱动程序和驱动程序堆栈中的其他驱动程序名为的 IRQL。 请考虑以下情况：

-   如果您的驱动程序在内核模式驱动程序堆栈的顶部，系统通常会调用驱动程序在 IRQL = 被动\_级别。 此类驱动程序的客户端可能基于 UMDF 驱动程序或用户模式应用程序。 指定**WdfExecutionLevelPassive**不会造成不利影响驱动程序的性能，因为框架不需要您的驱动程序调用的 IRQL 在调用工作项进行排队 = 被动\_级别。

-   如果您的驱动程序不是在堆栈的顶部，系统可能不会调用您的驱动程序在 IRQL = 被动\_级别。 因此，该框架必须排队驱动程序的调用的工作项，更高版本调用在 IRQL = 被动\_级别。 此过程可能会导致不佳的驱动程序的高性能，与允许在 IRQL 要调用的驱动程序的回调函数的比较&lt;= 调度\_级别。

为 DPC 对象和计时器对象不表示[被动级别计时器](using-timers.md)，请注意，不能设置**AutomaticSerialization**的配置结构的成员 **，则返回 TRUE**如果您具有父设备的执行级别设置为**WdfExecutionLevelPassive**。 这是因为框架将获取设备对象的[回调同步锁](using-framework-locks.md)在 IRQL = 被动\_级别，因此不能使用锁来同步 DPC 或计时器对象回调函数，其必须执行在 IRQL = 调度\_级别。 在这种情况下，您的驱动程序应使用[framework 自旋锁](using-framework-locks.md#framework-spin-locks)在任何设备、 DPC 或计时器对象回调函数中必须相互同步。

另请注意，为计时器对象的*做*表示被动级别计时器，您可以设置**AutomaticSerialization**为 TRUE 的配置结构的成员*唯一*如果父设备的执行级别设置为**WdfExecutionLevelPassive**。

 

 





