---
title: 线程 DPC 简介
description: 线程 DPC 简介
ms.assetid: 891a8a52-83ff-400a-9477-8edca1b9a83c
keywords:
- 线程的 Dpc WDK 内核
- 实时线程 WDK 内核
- 已占用的 Dpc WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc772ce20985eeb98a5f472464f200334444a010
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386585"
---
# <a name="introduction-to-threaded-dpcs"></a>线程 DPC 简介





线程的 Dpc 是在 Windows Vista 和更高版本的 Windows 中可用。

一个*线程 DPC*是 DPC，则系统将执行在 IRQL = 被动\_级别。 默认情况下，启用线程 dpc 进行标记，但你可以通过设置禁用它们**HKLM\\系统\\CCS\\控制\\SessionManager\\内核\\ThreadDpcEnable**为零的注册表项。 当线程的 Dpc 将被禁用时，它们将作为普通 Dpc 执行。

普通 DPC 抢先于所有线程的执行，并且不能由线程或由另一个 DPC 被取代。 如果系统有大量的普通 Dpc 排入队列，或在这些 Dpc 之一适用于较长时间运行，每个线程将保持暂停状态的任意长的时间。 因此，每个普通 DPC 会增加系统延迟，可能会降低性能时间敏感型应用程序，例如音频或视频播放。

相反，普通的 DPC，但不是受其他线程，则可以抢占线程的 DPC。 因此，应使用线程的 Dpc 而不是普通 Dpc-除非特定 DPC 必须不会被抢占，甚至不由另一个 DPC。

系统表示线程的 Dpc （和普通 dpc 进行标记） 作为[ **KDPC** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构。 若要初始化**KDPC**线程 DPC，调用的结构[ **KeInitializeThreadedDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializethreadeddpc)例程，并将其传递[ *CustomThreadedDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542976)执行 DPC 的操作的例程。

因为*CustomThreadedDpc*例程可以执行在任一被动\_级别或调度\_级别，您必须确保你*CustomThreadedDpc*例程正确在这两个于 Irql 同步。 有关如何执行此操作的详细信息，请参阅[同步和线程 Dpc](synchronization-and-threaded-dpcs.md)。

此外，您必须确保你*CustomThreadedDpc*例程服从所有的限制的调度\_级别代码。 如果启用了线程 dpc 进行标记，它们运行在 IRQL = 被动\_级别，但仍受到与普通 Dpc 相同的限制。 所有线程 DPC 中执行的代码，包括所有由调用的函数*CustomThreadedDpc*例程-必须符合 DPC 环境的限制。 例如，代码不能阻止对被动级别同步对象，如[KEVENT 对象](defining-and-using-an-event-object.md)。 大多数现有的设备堆栈，例如网络、 存储和 USB、 不支持线程的 DPC 处理，并且它们可能会尝试阻止如果检测到它们在被动调用\_级别。 出于类似原因[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF) 不支持线程的 DPC 处理，并且 KMDF 驱动程序不应尝试使用线程 dpc 进行标记。 有关 DPC 环境的详细信息，请参阅[写入 DPC 例程](writing-dpc-routines.md)。

若要添加到 DPC 队列的线程的 DPC，调用[ **KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)。 若要从队列中删除线程的 DPC 执行前，调用[ **KeRemoveQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovequeuedpc)。

 

 




