---
title: 使用框架锁
description: 使用框架锁
ms.assetid: d036a2d5-a9e9-4375-84b0-fbd797ee6f13
keywords:
- 同步 WDK KMDF
- 同步锁定 WDK KMDF
- 锁定 WDK KMDF
- 回调同步锁定 WDK KMDF
- 旋转锁 WDK KMDF
- 等待锁 WDK KMDF
- 中断锁 WDK KMDF
- framework 中断锁定 WDK KMDF
- framework 等待锁 WDK KMDF
- framework 数值调节钮锁定 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa124274bb6d6e7f39d1ff7d5754e78577b160e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372262"
---
# <a name="using-framework-locks"></a>使用框架锁


有时驱动程序必须提供驱动程序特定的 I/O 请求相关的回调函数，除了或替代框架提供同步的同步。 驱动程序可以使用回调同步锁、 旋转锁、 等待锁，并中断锁来同步驱动程序代码。

### <a name="callback-synchronization-locks"></a>回调同步锁

如果你已设置您的驱动程序以使用该框架[自动同步](using-automatic-synchronization.md)功能，该框架之前调用回调函数的驱动程序的 I/O 请求相关的事件获取同步锁。

这些*回调同步锁*，这与 framework 设备对象和队列对象相关联还不致由驱动程序。 若要获取同步锁，驱动程序调用[ **WdfObjectAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff548721)。 若要释放锁，驱动程序调用[ **WdfObjectReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff548765)。

你可能想您的驱动程序如果驱动程序使用的 I/O 请求相关的回调函数的框架的设备级或队列级别同步，但必须同步在 IRQL 运行一些代码，请使用回调同步锁 = 被动\_级别使用回叫函数，运行在 IRQL = 调度\_级别。 这是因为驱动程序可以使用自动同步仅对在相同的 IRQL 执行的回调函数。

例如，驱动程序可以使用自动同步为某个工作项的对象仅当工作项对象的父对象的执行级别为**WdfExecutionLevelPassive** （因为在始终执行工作项的回调函数IRQL = 被动\_级别)。 因此，如果指定了一个驱动程序**WdfExecutionLevelDispatch**中**ExecutionLevel**的设备对象的成员[ **WDF\_对象\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)结构，该驱动程序不能设置**AutomaticSerialization**子工作项对象的配置结构的成员。 相反，该驱动程序必须获取回调同步锁来同步[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)父设备对象的回调函数的回调函数。

### <a name="framework-wait-locks"></a>Framework 等待锁

使用框架等待锁来同步访问驱动程序数据在 IRQL 运行的代码从 = 被动\_级别。 驱动程序可以使用框架等待锁之前，必须调用[ **WdfWaitLockCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockcreate)创建等待锁对象。 然后，该驱动程序可以调用[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)获取的锁并[ **WdfWaitLockRelease** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockrelease)以将其释放。

### <a href="" id="framework-spin-locks"></a> Framework 自旋锁

Framework 自旋锁用于同步对驱动程序数据的访问，在 IRQL 运行的代码与&lt;= 调度\_级别。 当驱动程序线程获取旋转锁时，系统会将线程的 IRQL 设置为调度\_级别。 当线程释放锁时，系统会将线程的 IRQL 还原到以前的级别。

未使用自动 framework 同步的驱动程序可能使用旋转锁对访问进行同步的设备对象上下文空间，如果上下文空间是可写，并且如果有多个驱动程序的事件回调函数之一访问空间。

驱动程序才能使用 framework 旋转锁，必须调用[ **WdfSpinLockCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfspinlockcreate)创建旋转锁对象。 然后，该驱动程序可以调用[ **WdfSpinLockAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))获取的锁并[ **WdfSpinLockRelease** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))以将其释放。

自旋锁的用法示例，请参阅[同步发送请求的取消](synchronizing-cancellation-of-sent-requests.md)。

### <a name="framework-interrupt-locks"></a>Framework 中断锁

中断对象支持 DIRQL 的中断处理，framework 中断锁自旋锁。 您的驱动程序获取中断自旋锁后，该驱动程序将在设备的 DIRQL 执行，直到它释放锁。 有关使用中断锁的详细信息，请参阅[同步中断代码](synchronizing-interrupt-code.md)。

对于支持被动级别处理的中断对象，framework 中断锁是等待锁。 您的驱动程序获取中断等待锁后，驱动程序将执行在 IRQL = 被动\_级别直到它释放锁。 有关被动级别处理的详细信息，请参阅[支持被动中断级别](supporting-passive-level-interrupts.md)。

 

 





