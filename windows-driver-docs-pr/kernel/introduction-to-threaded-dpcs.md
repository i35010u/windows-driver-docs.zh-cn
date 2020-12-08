---
title: 线程 DPC 简介
description: 线程 DPC 简介
keywords:
- 线程 Dpc WDK 内核
- 实时线程 WDK 内核
- 已抢占 Dpc WDK 内核
ms.date: 01/23/2020
ms.localizationpriority: medium
ms.openlocfilehash: b2aa130eba38a1087732de76a958e95c9d4759bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838869"
---
# <a name="introduction-to-threaded-dpcs"></a>线程 DPC 简介

线程 Dpc 适用于 Windows Vista 和更高版本的 Windows。

*线程 dpc* 是指系统以 IRQL = 被动级别执行的 dpc \_ 。 线程 Dpc 默认情况下处于启用状态，但你可以通过将 **HKLM \\ System \\ CCS \\ Control \\ SessionManager \\ Kernel \\ ThreadDpcEnable** 注册表项设置为零来禁用它们。 禁用线程 Dpc 后，它们将作为普通 Dpc 来执行。

普通 DPC 抢先于所有线程的执行，不能被线程或其他 DPC 抢占。 如果系统中有大量普通 Dpc 处于排队状态，或者其中一个 Dpc 长时间运行，则每个线程都将在任意长时间内保持暂停状态。 因此，每个普通 DPC 会增加系统延迟，这可能会影响对时间敏感的应用程序（如音频或视频播放）的性能。

相反，可以使用普通的 DPC 而不是其他线程来抢占线程 DPC。 因此，除非特定 DPC 不能被抢占，甚至不能使用其他 DPC，否则应该使用线程 Dpc，而不是普通 dpc。

系统表示线程 Dpc (和普通 Dpc) 为 [**KDPC**](./eprocess.md) 结构。 若要为线程化 DPC 初始化 **KDPC** 结构，请调用 [**KeInitializeThreadedDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializethreadeddpc) 例程，并向其传递执行 DPC 操作的 [*CustomThreadedDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542976) 例程。

由于 *CustomThreadedDpc* 例程可以在被动 \_ 级别或调度 \_ 级别执行，因此必须确保 *CustomThreadedDpc* 例程在两个 IRQLs 上都正确同步。 有关如何执行此操作的详细信息，请参阅 [同步和线程 dpc](synchronization-and-threaded-dpcs.md)。

此外，还必须确保 *CustomThreadedDpc* 例程服从调度级别代码的所有限制 \_ 。 如果启用了线程 Dpc，它们会以 IRQL = 被动 \_ 级别运行，但仍受与普通 dpc 相同的限制。 在线程 DPC 中执行的所有代码（包括 *CustomThreadedDpc* 例程调用的所有函数）必须符合 DPC 环境的限制。 例如，代码不得在被动级同步对象（如 [KEVENT 对象](defining-and-using-an-event-object.md)）上阻塞。 许多现有的设备堆栈（如网络和 USB）不支持线程化的 DPC 处理，如果检测到它们在被动级别调用，它们可能会被阻止 \_ 。 由于类似的原因， [内核模式驱动程序框架](../wdf/index.md) (KMDF) 不支持线程化 DPC 处理，KMDF 驱动程序不应尝试使用线程 dpc。 有关 DPC 环境的详细信息，请参阅 [编写 DPC 例程](writing-dpc-routines.md)。

若要将线程 DPC 添加到 DPC 队列，请调用 [**KeInsertQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)。 若要从队列中删除线程化 DPC，请调用 [**KeRemoveQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovequeuedpc)。
