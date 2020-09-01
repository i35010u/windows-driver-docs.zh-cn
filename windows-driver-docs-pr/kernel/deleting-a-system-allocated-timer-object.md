---
title: 删除系统分配的计时器对象
description: 从 Windows 8.1 开始，ExDeleteTimer 例程将删除 ExAllocateTimer 例程创建的计时器对象。
ms.assetid: 7D119448-3890-4E8F-BC79-7FEB3213B693
keywords:
- ExXxxTimer 例程
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
- ExTimerDeleteCallback
- EX_TIMER
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8df4168c7aaeb418251d8ad4fedcab2ad7fb716
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185799"
---
# <a name="deleting-a-system-allocated-timer-object"></a>删除系统分配的计时器对象


从 Windows 8.1 开始， [**ExDeleteTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletetimer) 例程将删除 [**ExAllocateTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer) 例程创建的计时器对象。 此计时器对象是系统分配的 [**EX \_ 计时器**](./eprocess.md) 结构，其成员对于驱动程序是不透明的。 在删除计时器对象之前， **ExDeleteTimer** 将对该对象禁用进一步的计时器操作，并取消或完成可能正在进行的对象上的任何挂起的操作。

驱动程序调用 **ExDeleteTimer**后，此例程会执行几个步骤，以确保它可以安全删除计时器对象。 首先， **ExDeleteTimer** 将 timer 对象标记为禁用，以防止驱动程序启动使用对象的新计时器操作。 禁用计时器对象后，调用 [**ExSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer) 或 [**ExCancelTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excanceltimer) 例程会立即返回 **FALSE** ，并且不执行任何操作。 另外，对 **ExDeleteTimer** 的第二次调用返回 **FALSE** ，并且不执行任何操作。

接下来， **ExDeleteTimer** 将检查计时器是否仍在以前对 **ExDeleteTimer**的调用中挂起。 禁用计时器对象不会取消在禁用对象之前设置的计时器。 在以下两种情况下，在禁用计时器对象之后，先前设置的计时器可能会过期：

-   计时器为定期计时器。
-   计时器为一 (或非周期性) ，并且尚未过期。

计时器对象禁用后，定期计时器永不会永不过期。

如果你的驱动程序实现了 [*ExTimerCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_callback) 回调例程，则此例程的 *timer* 参数一定会始终是指向 timer 对象的有效指针 (**EX \_ 计时器** 结构) ，即使计时器对象禁用后计时器过期。

如果没有挂起的计时器， **ExDeleteTimer** 会删除计时器对象，并返回而不等待。

如果调用 **ExDeleteTimer** 时计时器处于挂起状态，则驱动程序向此例程提供的 *Cancel* 和 *Wait* 参数值控制例程的行为。 *Cancel*参数告诉**ExDeleteTimer**是否尝试取消挂起的计时器。 *Wait*参数告诉**ExDeleteTimer**是否等待返回，直到计时器对象被删除。

如果 *Cancel* 为 **false** (在这种情况下， *Wait* 必须为 **false**) 并且计时器处于挂起状态， **ExDeleteTimer** 让计时器在计时器对象删除之前过期。 在这种情况下， **ExDeleteTimer** 会标记 timer 对象，以指示该对象将在挂起的计时器过期后被删除 (并且对 *ExTimerCallback* 例程的任何最后回调都) 完成。 然后， **ExDeleteTimer** 返回，而不等待计时器完成过期或要删除的对象。

如果 *Cancel* 为 **TRUE**，则 **ExDeleteTimer** 将在挂起的计时器过期之前尝试取消该计时器。 如果**ExDeleteTimer**成功取消计时器，则返回**TRUE** 。 如果**ExDeleteTimer**不能取消计时器，则返回**FALSE** ，这是已过期或正在过期的一次拍摄计时器的情况。 如果在**ExDeleteTimer**调用之前取消了 (一步或定期) 计时器，或者从未设置过计时器， **ExDeleteTimer**也将返回**FALSE** 。

如果 *Cancel* 为 **TRUE** 且 *Wait* 为 **FALSE**，则 **ExDeleteTimer** 绝不会阻止调用线程。 如果无法立即删除 timer 对象， **ExDeleteTimer** 会标记 timer 对象，以指示在挂起的计时器完成过期后将其删除，并立即返回，而不等待计时器过期或对象被删除。

如果 *Cancel* 和 *Wait* 均 **为 TRUE**，则 **ExDeleteTimer** 会阻止调用线程（如果无法立即删除计时器对象）。 如有必要， **ExDeleteTimer**将等待计时器完成过期，并等待对驱动程序实现的*ExTimerCallback*例程的任何回调完成。 接下来，如果驱动程序实现此例程， **ExDeleteTimer** 将删除计时器对象并调用 [*ExTimerDeleteCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ext_delete_callback) 例程。 最后， **ExDeleteTimer** 返回。

驱动程序可以从驱动程序的*ExTimerCallback*例程调用**ExDeleteTimer** ，后者以 IRQL = 调度 \_ 级别运行，但驱动程序必须在此调用中将*Wait*参数设置为**FALSE**。

作为一个选项，驱动程序可以实现一个在删除计时器对象之后运行的 *ExTimerDeleteCallback* 回调例程。 通常情况下， *ExTimerDeleteCallback* 例程会释放驱动程序分配的用于计时器对象的任何系统资源。

**ExDeleteTimer** 计划在删除 timer 对象之后要运行的驱动程序实现的 *ExTimerDeleteCallback* 例程，此时该对象的指针不再有效。 如果**ExDeleteTimer**调用中的*Wait*参数为**TRUE** ，则*ExTimerDeleteCallback*例程的回调在**ExDeleteTimer**返回前完成。 如果 *Wait* 为 **FALSE**，则 *ExTimerDeleteCallback* 例程可能会在 **ExDeleteTimer** 返回之前或之后运行。

有关详细信息，请参阅 [Ex*Xxx*计时器例程和 ex \_ 计时器对象](exxxxtimer-routines-and-ex-timer-objects.md)。

 

