---
title: 视频微型端口驱动程序中的自旋锁
description: 视频微型端口驱动程序中的自旋锁
ms.assetid: 89ec0139-c109-44b1-aadd-a909a19ca1ee
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，自旋锁
- 旋转锁定 WDK 视频微型端口
- 锁定 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c879ca7d720e92b18bcb7aeeef1d5e7b594aa248
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066590"
---
# <a name="spin-locks-in-video-miniport-drivers"></a>视频微型端口驱动程序中的自旋锁


## <span id="ddk_spin_locks_in_video_miniport_drivers_gg"></span><span id="DDK_SPIN_LOCKS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


视频端口驱动程序支持视频微型端口驱动程序中的多处理器同步，方法是提供自旋锁函数，以便在一个或多个微型端口驱动程序线程以 IRQL 调度级别运行时保护数据 \_ 。 视频端口驱动程序的自旋锁函数使微型端口驱动程序线程能够创建、获取、释放和销毁旋转锁定。 视频端口驱动程序提供了这些功能，因为视频微型端口驱动程序编写器必须使用由视频端口驱动程序专门提供的函数来实现微型端口驱动程序。 有关自旋锁的一般讨论，请参阅 [自旋锁](../kernel/introduction-to-spin-locks.md)。

在视频微型端口驱动程序可以使用自旋锁之前，它必须通过调用 [**VideoPortCreateSpinLock**](/windows-hardware/drivers/ddi/video/nf-video-videoportcreatespinlock)来创建自旋锁。 创建自旋锁后，线程可以尝试通过调用 [**VideoPortAcquireSpinLock**](/previous-versions/ff570175(v=vs.85)) 或 [**VideoPortAcquireSpinLockAtDpcLevel**](/previous-versions/ff570176(v=vs.85))获取自旋锁。 当微型端口驱动程序的线程处于或低于 IRQL 调度级别时，可以使用此对的第一个函数 \_ 。 仅当线程以 IRQL 调度级别运行时，才能使用第二个函数 \_ 。

当持有自旋锁的线程完成了其任务后，微型端口驱动程序应释放旋转锁。 如果线程在对 **VideoPortAcquireSpinLock**的调用中获取了自旋锁，则它应使用 [**VideoPortReleaseSpinLock**](/previous-versions/ff570357(v=vs.85)) 释放旋转锁。 在对**VideoPortReleaseSpinLock**的调用中，当线程返回时，该线程必须在**VideoPortAcquireSpinLock**的*OldIrql*参数中收到的*NewIrql*参数中传递相同的值。 如果名为 **VideoPortAcquireSpinLockAtDpcLevel**的线程，则它应调用 [**VideoPortReleaseSpinLockFromDpcLevel**](/previous-versions/ff570358(v=vs.85)) 以释放旋转锁。

当微型端口驱动程序不再进一步使用自旋锁时，它应通过调用 [**VideoPortDeleteSpinLock**](/windows-hardware/drivers/ddi/video/nf-video-videoportdeletespinlock)来销毁旋转锁。

 

