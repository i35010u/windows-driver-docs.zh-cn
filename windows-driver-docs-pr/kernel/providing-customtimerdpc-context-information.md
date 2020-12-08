---
title: 提供 CustomTimerDpc 上下文信息
description: 提供 CustomTimerDpc 上下文信息
keywords:
- timer 对象 WDK 内核，CustomTimerDpc 例程
- CustomTimerDpc
- DeferredContext 例程
- 上下文信息 WDK 同步
- 计时器对象 WDK 内核，上下文信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5e1a1bcda198c7a48aa1e68efc33abfe84a85e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805389"
---
# <a name="providing-customtimerdpc-context-information"></a>提供 CustomTimerDpc 上下文信息





传递给 [**KeInitializeDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)的 *DeferredContext* 指针指向其他驱动程序例程和 *CustomTimerDpc* 例程本身可以保持状态的上下文区域。 内核通过每次调用 DPC 例程传递 *DeferredContext* 指针。

与 *IoTimer* 例程不同， *CustomTimerDpc* 与驱动程序创建的设备对象没有特定的关联。 但是，驱动程序可以通过在其上下文区中包含指向设备对象的指针，将 *CustomTimerDpc* 例程与驱动程序创建的设备对象相关联。

上下文区域必须位于驻留的、驱动程序分配的内存中。 通常，此上下文区域位于设备扩展中，但也可以位于非分页池中。 如果驱动程序使用控制器对象，则它可以在控制器扩展中。 上下文区域的内容由驱动程序确定。

如果 *CustomTimerDpc* 例程与驱动程序的 ISR 共享上下文信息，则 *CustomTimerDpc* 例程必须使用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 调用访问共享上下文的 *SynchCritSection* 例程。 有关详细信息，请参阅 [使用关键部分](using-critical-sections.md)。

如果 *CustomTimerDpc* 与其他非 ISR 驱动程序例程共享上下文信息，则必须通过执行人员旋转锁来保护 *DeferredContext* 上的区域。 有关详细信息，请参阅 [自旋锁](./introduction-to-spin-locks.md)。

 

