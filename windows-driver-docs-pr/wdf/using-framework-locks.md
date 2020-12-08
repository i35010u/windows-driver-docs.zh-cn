---
title: 使用框架锁
description: 使用框架锁
keywords:
- 同步 WDK KMDF
- 同步锁定 WDK KMDF
- 锁定 WDK KMDF
- 回调同步会锁定 WDK KMDF
- 旋转锁 WDK KMDF
- 等待锁定 WDK KMDF
- 中断锁定 WDK KMDF
- 框架中断锁定 WDK KMDF
- framework 等待锁定 WDK KMDF
- framework 旋转锁 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d130ab0759c75ecf8d6969af720f471d5e72704
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838709"
---
# <a name="using-framework-locks"></a>使用框架锁


有时，驱动程序必须提供与 i/o 请求相关的回调函数的特定于驱动程序的同步，或者除了或替换为框架提供的同步。 驱动程序可以使用回调同步锁、自旋锁、等待锁和中断锁来同步驱动程序代码。

### <a name="callback-synchronization-locks"></a>回调同步锁

如果已将驱动程序设置为使用框架的 [自动同步](using-automatic-synchronization.md) 功能，则在调用驱动程序的 i/o 请求相关事件回调函数之前，框架将获取同步锁。

与框架设备对象和队列对象相关联的这些 *回拨同步锁* 也可由驱动程序获取。 若要获取同步锁，驱动程序将调用 [**WdfObjectAcquireLock**](/previous-versions/ff548721(v=vs.85))。 若要释放锁，驱动程序将调用 [**WdfObjectReleaseLock**](/previous-versions/ff548765(v=vs.85))。

如果驱动程序使用框架的设备级别或队列级别的 i/o 请求相关回调函数的同步，但必须将以 irql = 被动级别运行的代码 \_ 与以 irql = 调度级别运行的回调函数同步，则你可能希望驱动程序使用回调同步锁定 \_ 。 这是因为，驱动程序只能对以相同的 IRQL 执行的回调函数使用自动同步。

例如，仅当工作项对象的父对象的执行级别是 **WdfExecutionLevelPassive** (的情况下，驱动程序才能使用自动同步，因为工作项的回调函数始终以 IRQL = 被动 \_ 级别) 执行。 因此，如果驱动程序在设备对象的 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构的 **ExecutionLevel** 成员中指定 **WdfExecutionLevelDispatch** ，则驱动程序将无法设置子工作项对象的配置结构的 **AutomaticSerialization** 成员。 相反，驱动程序必须获取回调同步锁，才能将 [*EvtWorkItem*](/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) 回调函数与父设备对象的回调函数同步。

### <a name="framework-wait-locks"></a>Framework 等待锁

使用 framework 等待锁来同步对从 IRQL = 被动级别运行的代码的驱动程序数据的访问 \_ 。 在驱动程序可以使用框架等待锁定之前，它必须调用 [**WdfWaitLockCreate**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate) 来创建等待锁定对象。 然后，该驱动程序可以调用 [**WdfWaitLockAcquire**](/previous-versions/ff551168(v=vs.85)) 来获取锁，并 [**WdfWaitLockRelease**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease) 将其释放。

### <a name="framework-spin-locks"></a><a href="" id="framework-spin-locks"></a> Framework 旋转锁

使用框架旋转锁来同步对以 IRQL = 调度级别运行的代码的驱动程序数据的访问 &lt; \_ 。 当驱动程序线程获取旋转锁时，系统会将该线程的 IRQL 设置为调度 \_ 级别。 当线程释放锁定时，系统会将该线程的 IRQL 还原到其以前的级别。

如果上下文空间是可写的，并且如果有多个驱动程序的事件回调函数访问空间，则没有使用自动 framework 同步的驱动程序可能使用旋转锁来同步对设备对象的上下文空间的访问。

在驱动程序可以使用框架旋转锁之前，它必须调用 [**WdfSpinLockCreate**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate) 来创建旋转锁定对象。 然后，该驱动程序可以调用 [**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) 来获取锁，并 [**WdfSpinLockRelease**](/previous-versions/windows/hardware/drivers/ff550044(v=vs.85)) 将其释放。

有关使用旋转锁的示例，请参阅 [同步取消已发送请求](synchronizing-cancellation-of-sent-requests.md)。

### <a name="framework-interrupt-locks"></a>框架中断锁

对于支持 DIRQL 中断处理的中断对象，框架中断锁是自旋锁。 驱动程序获取中断自旋锁后，驱动程序将在设备的 DIRQL 上执行，直到释放该锁。 有关使用中断锁的详细信息，请参阅 [同步中断代码](synchronizing-interrupt-code.md)。

对于支持被动级别处理的中断对象，框架中断锁是等待锁定。 当驱动程序获取中断等待锁定后，该驱动程序将以 IRQL = 被动级别执行， \_ 直到释放该锁。 有关被动级别处理的详细信息，请参阅 [支持被动级别中断](supporting-passive-level-interrupts.md)。

 

