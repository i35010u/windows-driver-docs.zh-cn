---
title: 排队的自旋锁
description: 排队的自旋锁
ms.assetid: 7ccec366-5436-4e69-9fb7-f0090cf2adcb
keywords:
- 排队自旋锁 WDK 内核
- 第一次提供的自旋锁
- KeAcquireInStackQueuedSpinLock
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eab4518863f437a054f4a16ef81727f8ac1306aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838479"
---
# <a name="queued-spin-locks"></a>排队的自旋锁





*排队自旋锁*是自旋锁的变体，在多处理器计算机上更高效地进行争用锁定。 在多处理器计算机上，使用排队的自旋锁可保证处理器先按首先处理的方式获取自旋锁。 适用于 Windows XP 和更高版本 Windows 的驱动程序应使用排队自旋锁，而不是普通的旋转锁。

驱动程序为自旋锁提供存储，并将其初始化为[**KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)。 驱动程序使用[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))获取排队自旋锁，并使用[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)将其释放。

驱动程序将通过指向**KeAcquireInStackQueuedSpinLock**的指针传递[ **\_句柄结构来分配 KLOCK\_队列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)。 驱动程序在释放旋转锁时，通过指向**KeReleaseInStackQueuedSpinLock**的指针传递相同的结构。 通常，在每次获取锁定时，驱动程序都应在堆栈上分配结构。

驱动程序不得将对排队自旋锁例程和普通**Ke*Xxx*旋转锁**例程的调用混合到同一个自旋锁上。

如果驱动程序已经处于 IRQL =\_级别，则它可以改为调用[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))和[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel) 。

 

 




