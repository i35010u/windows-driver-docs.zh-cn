---
title: WavePci 微型端口驱动程序的可靠性问题
description: WavePci 微型端口驱动程序的可靠性问题
ms.assetid: 329f28a8-5e99-4c25-8a88-1e634f7eeec8
keywords:
- WavePci 可靠性问题 WDK 音频
- 旋转锁定 WDK 音频
- 正在取消 Irp
- 死锁 WDK 音频
- 中断服务例程 WDK 音频
- Isr WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd2b0f8b12ddc4a70b1cedc789155920ad0ff55c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832436"
---
# <a name="reliability-issues-for-a-wavepci-miniport-driver"></a>WavePci 微型端口驱动程序的可靠性问题


## <span id="reliability_issues_for_a_wavepci_miniport_driver"></span><span id="RELIABILITY_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


WavePci 微型端口驱动程序必须跟踪它从端口驱动程序接收到的映射。 WavePci 微型端口驱动程序会在驱动程序线程之间共享的数据结构中维护其映射列表。 驱动程序线程还必须共享对 DMA 通道的访问权限，以便向硬件队列添加新映射并从队列中删除已完成的映射。 为了防止数据损坏，微型端口驱动程序使用自旋锁来序列化对共享数据结构和外围设备的访问。 旋转锁定可防止两个或多个驱动程序线程同时访问共享数据和硬件队列。

在开发管理映射的驱动程序部分时，供应商应特别注意以下几点。

### <a name="span-idspin_locksspanspan-idspin_locksspanspan-idspin_locksspanspin-locks"></a><span id="Spin_Locks"></span><span id="spin_locks"></span><span id="SPIN_LOCKS"></span>旋转锁

若要避免潜在的死锁，微型端口驱动程序在调用 Portcls 以获取或释放映射时不得持有自己的自旋锁。 Microsoft Windows 驱动程序工具包（WDK）中的 Ac97 示例驱动程序说明了此原则。 在调用[**IPortWavePciStream：： GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)或[**IPortWavePciStream：： ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping)之前，示例驱动程序调用[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)以释放旋转锁。 在**GetMapping**或**ReleaseMapping**调用返回后，该驱动程序将调用[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)再次获取自旋锁。 在调用以释放和获取旋转锁之间，驱动程序线程不能假定它具有对映射列表的独占访问权限。 在此未受保护的时间间隔内访问共享数据是危险的。 如果释放和获取自旋锁之间的时间间隔很小，则两个驱动程序线程之间的争用条件导致数据损坏的可能性也很小。 这意味着生成的失败是间歇性的，因而难以跟踪。 释放并获取旋转锁后，编写完善的驱动程序应假设它以前用于访问共享数据结构的内容的任何临时指针或索引都不再有效。

### <a name="span-idirp_cancellationspanspan-idirp_cancellationspanspan-idirp_cancellationspanirp-cancellation"></a><span id="IRP_Cancellation"></span><span id="irp_cancellation"></span><span id="IRP_CANCELLATION"></span>IRP 取消

在处理播放或捕获流的过程中，取消 IRP 会导致操作系统吊销微型端口驱动程序已获取的一个或多个映射。 发生这种情况时，端口驱动程序会调用[**IMiniportWavePciStream：： RevokeMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-revokemappings)方法来通知微型端口驱动程序。 为了避免将数据从或捕获到吊销的映射中，小型端口驱动程序必须删除其软件列表和 DMA 控制器的硬件队列中的映射。 由于软件列表和硬件队列是在驱动程序线程之间共享的，因此需要小心执行这些操作。

例如，要撤消的一组映射可能包含刚刚或即将发布的映射。 在这种情况下，两个驱动程序线程可能同时尝试从 DMA 队列中删除相同的映射。 如果驱动程序无法阻止同时访问，则结果可能会损坏管理队列的寄存器或内存结构中的数据。

有关工作代码示例，请参阅 Windows 驱动程序工具包（WDK）中的 Ac97 示例驱动程序。

 

 




