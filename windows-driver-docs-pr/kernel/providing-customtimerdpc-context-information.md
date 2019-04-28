---
title: 提供 CustomTimerDpc 上下文信息
description: 提供 CustomTimerDpc 上下文信息
ms.assetid: b4d711fb-63d4-45c6-8054-f934741ce340
keywords:
- 计时器对象 WDK 内核，CustomTimerDpc 例程
- CustomTimerDpc
- DeferredContext 例程
- WDK 同步的上下文信息
- 计时器对象 WDK 内核，上下文信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b616ad73439601e072b8f0238f6b76d5497a73f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338544"
---
# <a name="providing-customtimerdpc-context-information"></a>提供 CustomTimerDpc 上下文信息





*DeferredContext*指针传递给[ **KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130)指向上下文区域的其他驱动程序、 例程和*CustomTimerDpc*例程本身，可以维护状态。 内核将传递*DeferredContext* DPC 例程的每个调用中的指针。

与不同*IoTimer*例程*CustomTimerDpc*具有与驱动程序创建的设备对象没有特定关联。 但是，驱动程序可以将相关联*CustomTimerDpc*例程与驱动程序创建的设备对象通过在其上下文区域内包含指向设备对象的指针。

上下文区域必须在内存中驻留时，将驱动程序分配。 通常情况下，此上下文区域是在设备扩展中，但也可以是在非分页缓冲池。 如果该驱动程序使用的控制器对象，它可以是控制器扩展。 上下文区域的内容都由驱动程序确定。

如果*CustomTimerDpc*例程与驱动程序的 ISR 共享上下文信息*CustomTimerDpc*例程必须使用[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)来调用*SynchCritSection*例程访问的共享的上下文。 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

如果*CustomTimerDpc*共享上下文信息与其他非 ISR 驱动程序例程位于区域*DeferredContext*必须通过执行旋转锁保护。 有关详细信息，请参阅[旋转锁](spin-locks.md)。

 

 




