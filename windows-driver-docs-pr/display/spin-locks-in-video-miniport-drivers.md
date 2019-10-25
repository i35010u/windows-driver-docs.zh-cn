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
ms.openlocfilehash: 468b886a0bc6d7650c7e41bed749ac7974f73840
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825711"
---
# <a name="spin-locks-in-video-miniport-drivers"></a>视频微型端口驱动程序中的自旋锁


## <span id="ddk_spin_locks_in_video_miniport_drivers_gg"></span><span id="DDK_SPIN_LOCKS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


视频端口驱动程序支持视频微型端口驱动程序中的多处理器同步，方法是在一个或多个微型端口驱动程序线程以 IRQL 调度\_级别运行时，通过提供自旋锁函数来保护数据。 视频端口驱动程序的自旋锁函数使微型端口驱动程序线程能够创建、获取、释放和销毁旋转锁定。 视频端口驱动程序提供了这些功能，因为视频微型端口驱动程序编写器必须使用由视频端口驱动程序专门提供的函数来实现微型端口驱动程序。 有关自旋锁的一般讨论，请参阅[自旋锁](https://docs.microsoft.com/windows-hardware/drivers/kernel/spin-locks)。

在视频微型端口驱动程序可以使用自旋锁之前，它必须通过调用[**VideoPortCreateSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcreatespinlock)来创建自旋锁。 创建自旋锁后，线程可以尝试通过调用[**VideoPortAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff570175)或[**VideoPortAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff570176)获取自旋锁。 当微型端口驱动程序的线程达到或低于 IRQL 调度\_级别时，可以使用此对的第一个函数。 仅当线程以 IRQL 调度\_级别运行时，才能使用第二个函数。

当持有自旋锁的线程完成了其任务后，微型端口驱动程序应释放旋转锁。 如果线程在对**VideoPortAcquireSpinLock**的调用中获取了自旋锁，则它应使用[**VideoPortReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff570357)释放旋转锁。 在对**VideoPortReleaseSpinLock**的调用中，当线程返回时，该线程必须在**VideoPortAcquireSpinLock**的*OldIrql*参数中收到的*NewIrql*参数中传递相同的值。 如果名为**VideoPortAcquireSpinLockAtDpcLevel**的线程，则它应调用[**VideoPortReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff570358)以释放旋转锁。

当微型端口驱动程序不再进一步使用自旋锁时，它应通过调用[**VideoPortDeleteSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportdeletespinlock)来销毁旋转锁。

 

 





