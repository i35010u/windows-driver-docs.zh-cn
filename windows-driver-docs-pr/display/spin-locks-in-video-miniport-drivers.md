---
title: 视频微型端口驱动程序中的自旋锁
description: 视频微型端口驱动程序中的自旋锁
ms.assetid: 89ec0139-c109-44b1-aadd-a909a19ca1ee
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，自旋锁
- 数值调节钮锁 WDK 微型端口
- 锁定 WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b69ca114bf6e01f930d8ad1dfdb80ee35000e6eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381809"
---
# <a name="spin-locks-in-video-miniport-drivers"></a>视频微型端口驱动程序中的自旋锁


## <span id="ddk_spin_locks_in_video_miniport_drivers_gg"></span><span id="DDK_SPIN_LOCKS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


通过提供数值调节钮的锁函数，以保护数据时一个微型端口驱动程序中的视频端口驱动程序支持多处理器同步或更多的微型端口驱动程序线程正在运行或以下的 IRQL 调度\_级别。 视频端口驱动程序的数值调节钮的锁函数启用微型端口驱动程序线程以创建、 获取、 发布并销毁自旋锁。 视频端口驱动程序提供这些函数，因为微型端口驱动程序编写器必须实现微型端口驱动程序使用的视频端口驱动程序以独占方式提供的函数。 自旋锁的常规讨论，请参阅[自旋锁](https://msdn.microsoft.com/library/windows/hardware/ff563830)。

微型端口驱动程序可以使用旋转锁之前，它必须通过调用创建旋转锁[ **VideoPortCreateSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff570289)。 一个线程创建旋转锁后，可以尝试通过调用获取自旋锁[ **VideoPortAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff570175)或[ **VideoPortAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff570176)。 可以使用此对的第一个函数，当微型端口驱动程序的线程或以下的 IRQL 调度\_级别。 只有当线程在 IRQL 调度运行时，可以使用第二个函数\_级别。

当持有自旋锁而使线程完成其任务时，微型端口驱动程序应释放自旋锁。 如果线程获取对的调用中旋转锁**VideoPortAcquireSpinLock**，它应使用[ **VideoPortReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff570357)释放自旋锁。 在调用**VideoPortReleaseSpinLock**，线程必须通过在相同的值*NewIrql*参数中接收*OldIrql* 参数**VideoPortAcquireSpinLock**该函数返回时。 如果该线程调用**VideoPortAcquireSpinLockAtDpcLevel**，则应调用[ **VideoPortReleaseSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff570358)释放自旋锁。

当微型端口驱动程序没有进一步用于旋转锁时，它应通过调用销毁自旋锁[ **VideoPortDeleteSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff570293)。

 

 





