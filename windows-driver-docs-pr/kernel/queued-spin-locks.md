---
title: 排队的自旋锁
description: 排队的自旋锁
keywords:
- 排队自旋锁 WDK 内核
- 第一次提供的自旋锁
- KeAcquireInStackQueuedSpinLock
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb0493944c6b6ba4cb3544bc01fa167724e8863
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805375"
---
# <a name="queued-spin-locks"></a>排队的自旋锁





*排队自旋锁* 是自旋锁的变体，在多处理器计算机上更高效地进行争用锁定。 在多处理器计算机上，使用排队的自旋锁可保证处理器先按首先处理的方式获取自旋锁。 适用于 Windows XP 和更高版本 Windows 的驱动程序应使用排队自旋锁，而不是普通的旋转锁。

驱动程序为自旋锁提供存储，并将其初始化为 [**KeInitializeSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)。 驱动程序使用 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 获取排队自旋锁，并使用 [**KeReleaseInStackQueuedSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 将其释放。

驱动程序分配一个 [**KLOCK \_ 队列 \_ 句柄**](./eprocess.md) 结构，该结构由指向 **KeAcquireInStackQueuedSpinLock** 的指针传递。 驱动程序在释放旋转锁时，通过指向 **KeReleaseInStackQueuedSpinLock** 的指针传递相同的结构。 通常，在每次获取锁定时，驱动程序都应在堆栈上分配结构。

驱动程序不得将对排队自旋锁例程和普通 **Ke *Xxx* 旋转锁** 例程的调用混合到同一个自旋锁上。

如果驱动程序已经处于 IRQL = 调度 \_ 级别，则它可以改为调用 [**KeAcquireInStackQueuedSpinLockAtDpcLevel**](/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)) 和 [**KeReleaseInStackQueuedSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel) 。

 

