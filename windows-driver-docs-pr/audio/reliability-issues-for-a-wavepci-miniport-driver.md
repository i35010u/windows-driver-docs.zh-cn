---
title: WavePci 微型端口驱动程序的可靠性问题
description: WavePci 微型端口驱动程序的可靠性问题
ms.assetid: 329f28a8-5e99-4c25-8a88-1e634f7eeec8
keywords:
- WavePci 可靠性问题 WDK 音频
- 数值调节钮锁 WDK 音频
- 正在取消 Irp
- 死锁 WDK 音频
- 中断服务例程 WDK 音频
- Isr WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1606cf3ba0e4c557fddb865e0f4e25bf52b0190b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328703"
---
# <a name="reliability-issues-for-a-wavepci-miniport-driver"></a>WavePci 微型端口驱动程序的可靠性问题


## <span id="reliability_issues_for_a_wavepci_miniport_driver"></span><span id="RELIABILITY_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


WavePci 微型端口驱动程序必须跟踪的接收端口驱动程序中的映射。 WavePci 微型端口驱动程序维护其驱动程序线程之间共享的数据结构中的映射的列表。 驱动程序线程还必须共享访问 DMA 通道以将新的映射添加到硬件队列和从队列中删除已完成的映射。 若要防止数据损坏，微型端口驱动程序使用自旋锁进行序列化对共享的数据结构和外围设备的访问。 旋转锁可防止共享的数据和硬件队列同时访问两个或多个驱动程序线程。

在开发时管理映射的驱动程序的一部分，供应商也需要特别注意以下几点。

### <a name="span-idspinlocksspanspan-idspinlocksspanspan-idspinlocksspanspin-locks"></a><span id="Spin_Locks"></span><span id="spin_locks"></span><span id="SPIN_LOCKS"></span>自旋锁

若要避免潜在的死锁，微型端口驱动程序不得保留数值调节钮锁定 Portcls.sys 获取或释放映射到调用时。 Ac97 示例驱动程序中 Microsoft Windows Driver Kit (WDK) 说明了这一原则。 之前调用[ **IPortWavePciStream::GetMapping** ](https://msdn.microsoft.com/library/windows/hardware/ff536909)或[ **IPortWavePciStream::ReleaseMapping**](https://msdn.microsoft.com/library/windows/hardware/ff536911)，示例驱动程序调用[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)释放自旋锁。 之后**GetMapping**或**ReleaseMapping**调用返回时，驱动程序调用[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)再次获取自旋锁。 释放和获取自旋锁的调用，之间驱动程序线程必须假定它具有对映射的列表的独占访问。 在此不受保护的时间间隔期间访问共享的数据是很危险。 如果释放和获取数值调节钮锁之间的间隔小，也是小型的两个驱动程序线程之间的争用条件被损坏的数据的可能性。 这意味着，产生的故障是间歇性的因此很难跟踪。 后释放和获取旋转锁，编写良好的驱动程序应假定任何临时指针或它以前用来访问共享的数据结构的内容的索引将不再有效。

### <a name="span-idirpcancellationspanspan-idirpcancellationspanspan-idirpcancellationspanirp-cancellation"></a><span id="IRP_Cancellation"></span><span id="irp_cancellation"></span><span id="IRP_CANCELLATION"></span>IRP 取消

在播放或捕获的流的处理过程中，随时取消的 IRP 可能会导致操作系统撤消已获取微型端口驱动程序的一个或多个映射。 当发生这种情况时，端口驱动程序会调用[ **IMiniportWavePciStream::RevokeMappings** ](https://msdn.microsoft.com/library/windows/hardware/ff536730)方法以通知微型端口驱动程序。 若要吊销映射到避免播放数据或捕获的数据，微型端口驱动程序必须从其软件列表和 DMA 控制器的硬件队列中删除映射。 由于软件列表和硬件队列驱动程序线程间共享，因此谨慎一些需要可靠地执行这些操作。

例如，映射以可撤消的一组可能包含了或几乎要释放的映射。 在这种情况下，两个驱动程序线程可能会同时尝试从 DMA 队列中删除相同的映射。 如果驱动程序无法防止同时访问，则结果可以是寄存器或内存中结构的管理队列中的数据损坏。

有关工作代码示例，请参阅 Ac97 示例驱动程序 Windows Driver Kit (WDK) 中。

 

 




