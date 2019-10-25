---
title: 使用框架锁
description: 使用框架锁
ms.assetid: d036a2d5-a9e9-4375-84b0-fbd797ee6f13
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
ms.openlocfilehash: 106603e3ad46679553896d7b3a9b6c8a65c3985c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843086"
---
# <a name="using-framework-locks"></a>使用框架锁


有时，驱动程序必须提供与 i/o 请求相关的回调函数的特定于驱动程序的同步，或者除了或替换为框架提供的同步。 驱动程序可以使用回调同步锁、自旋锁、等待锁和中断锁来同步驱动程序代码。

### <a name="callback-synchronization-locks"></a>回调同步锁

如果已将驱动程序设置为使用框架的[自动同步](using-automatic-synchronization.md)功能，则在调用驱动程序的 i/o 请求相关事件回调函数之前，框架将获取同步锁。

与框架设备对象和队列对象相关联的这些*回拨同步锁*也可由驱动程序获取。 若要获取同步锁，驱动程序将调用[**WdfObjectAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff548721)。 若要释放锁，驱动程序将调用[**WdfObjectReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff548765)。

如果驱动程序使用框架的设备级别或队列级别的 i/o 请求相关回调函数的同步，但必须同步某些在 IRQL = 被动的代码，则您可能希望您的驱动程序使用回调同步锁\_具有在 IRQL = 调度\_级别上运行的回调函数的级别。 这是因为，驱动程序只能对以相同的 IRQL 执行的回调函数使用自动同步。

例如，仅当工作项对象的父对象的执行级别为**WdfExecutionLevelPassive** （因为工作项的回调函数始终以 IRQL = 被动\_执行级别时，驱动程序才能对工作项对象使用自动同步。级别）。 因此，如果驱动程序在设备对象的[**WDF\_对象\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构的**ExecutionLevel**成员中指定了**WdfExecutionLevelDispatch** ，则驱动程序将无法设置**AutomaticSerialization**子工作项对象的配置结构的成员。 相反，驱动程序必须获取回调同步锁，才能将[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数与父设备对象的回调函数同步。

### <a name="framework-wait-locks"></a>Framework 等待锁

使用 framework 等待锁来同步对从 IRQL = 被动\_级别运行的代码的驱动程序数据的访问。 在驱动程序可以使用框架等待锁定之前，它必须调用[**WdfWaitLockCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate)来创建等待锁定对象。 然后，该驱动程序可以调用[**WdfWaitLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)来获取锁，并[**WdfWaitLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)将其释放。

### <a href="" id="framework-spin-locks"></a>Framework 旋转锁

使用框架旋转锁来同步从以 IRQL &lt;= 调度\_级别运行的代码对驱动程序数据的访问。 当驱动程序线程获取旋转锁时，系统会将该线程的 IRQL 设置为调度\_级别。 当线程释放锁定时，系统会将该线程的 IRQL 还原到其以前的级别。

如果上下文空间是可写的，并且如果有多个驱动程序的事件回调函数访问空间，则没有使用自动 framework 同步的驱动程序可能使用旋转锁来同步对设备对象的上下文空间的访问。

在驱动程序可以使用框架旋转锁之前，它必须调用[**WdfSpinLockCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate)来创建旋转锁定对象。 然后，该驱动程序可以调用[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))来获取锁，并[**WdfSpinLockRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))将其释放。

有关使用旋转锁的示例，请参阅[同步取消已发送请求](synchronizing-cancellation-of-sent-requests.md)。

### <a name="framework-interrupt-locks"></a>框架中断锁

对于支持 DIRQL 中断处理的中断对象，框架中断锁是自旋锁。 驱动程序获取中断自旋锁后，驱动程序将在设备的 DIRQL 上执行，直到释放该锁。 有关使用中断锁的详细信息，请参阅[同步中断代码](synchronizing-interrupt-code.md)。

对于支持被动级别处理的中断对象，框架中断锁是等待锁定。 驱动程序获取中断等待锁定后，该驱动程序将在%\_级别执行，直到释放该锁。 有关被动级别处理的详细信息，请参阅[支持被动级别中断](supporting-passive-level-interrupts.md)。

 

 





