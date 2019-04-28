---
title: 同步中断代码
description: 同步中断代码
ms.assetid: a24477dc-f75d-4ab6-8695-d8a85247e276
keywords:
- 硬件中断 WDK KMDF，同步
- 中断 WDK KMDF，同步
- 同步 WDK 中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d6a2996bcd901435c1f95f136434bc690884618
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350655"
---
# <a name="synchronizing-interrupt-code"></a>同步中断代码


以下因素使处理多处理器系统上的硬件中断的驱动程序代码变得复杂：

-   设备会中断，每次它提供的是易失性的因为它可以被覆盖，设备中断的下一步时间中断特定的信息。

-   在相对较高于 Irql 和其中断服务例程 (Isr) 设备中断可能会中断其他驱动程序代码的执行。

-   对于 DIRQL 中断 ISR 必须运行在 DIRQL 在持有驱动程序所提供的自旋锁，以便 ISR 可以阻止其他中断，虽然它省去了易失性的信息。 DIRQL 由当前的处理器，防止中断并旋转锁防止中断由另一个处理器。

-   ISR 必须快速运行，因为设备无法中断执行 ISR 时。 长 ISR 执行时间可能会减慢系统或可能会导致数据丢失。

-   ISR 和延迟的过程调用 (DPC) 例程通常必须访问 ISR 在其中存储设备的易失性数据的存储区域。 这些例程必须与彼此同步，以便它们不在同一时间访问存储区域。

由于所有这些因素，编写驱动程序代码来处理中断时，必须使用以下规则：

-   仅[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数可以访问易失性中断数据，例如设备注册包含中断的信息。

    [ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数应移动到驱动程序定义中断数据的易失性数据缓冲区的驱动程序[ *EvtInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数[ *EvtInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh406422)回调函数或多个[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)回调函数可以访问。

    如果您的驱动程序提供了[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh406422)及其中断对象，最佳的回调函数存储中断数据位置是中断对象[上下文空间](framework-object-context-space.md)。 中断对象的回调函数可以通过使用他们接收的对象句柄访问对象的上下文空间。

    如果您的驱动程序提供了多个[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)回调函数为每个[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)可能回调函数将中断数据存储在每个 DPC 对象的上下文空间。

-   必须同步访问中断数据缓冲区的所有驱动程序代码，以便只有一个例程一次访问数据。

    对于 DIRQL 中断对象， [ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数可以访问此数据缓冲区的 IRQL = DIRQL 按住中断对象的驱动程序所提供的自旋锁。 因此，访问缓冲区中的所有例程也必须都运行在 DIRQL 按住自旋锁。 (通常情况下，中断的[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)回调函数是仅其他例程必须访问缓冲区。）

    所有访问除中断数据缓冲区的例程[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数，必须执行下列操作之一：

    -   调用[ **WdfInterruptSynchronize** ](https://msdn.microsoft.com/library/windows/hardware/ff547389)计划[ *EvtInterruptSynchronize* ](https://msdn.microsoft.com/library/windows/hardware/ff541742)访问中断的回调函数数据缓冲区。
    -   访问调用之间的中断数据缓冲区的代码放[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)并[ **WdfInterruptReleaseLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547376).

    这两种方法允许[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)按住访问中断数据在 DIRQL 函数中断的自旋锁。 DIRQL 由当前的处理器，防止中断并旋转锁防止中断由另一个处理器。

    如果你的设备支持多个中断向量或消息，并且如果你想要同步的这些中断您的驱动程序处理，可以将单一自旋锁分配给多个 DIRQL 中断对象。 框架确定的一套中断，最高 DIRQL 和它始终将获取在该 DIRQL 自旋锁，以便同步的代码不能中断的任何中断向量或一组中的消息。

    有关[被动级别中断对象](supporting-passive-level-interrupts.md)，框架调用的驱动程序之前获取被动级别中断锁[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数在 IRQL = 被动\_级别。 因此，所有访问缓冲区的例程必须获取中断锁或在内部同步缓冲区的访问。 通常情况下，中断的[ *EvtInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh406422)回调函数是仅其他例程访问缓冲区。 了解如何获取从中断锁*EvtInterruptWorkItem*回调函数中，请参阅该页面的备注部分。

    你还可以通过将单个等待锁分配给多个被动级别中断对象同步您的驱动程序处理的多个中断向量。

-   如果某些您处理 DIRQL 中断的代码都必须运行在 IRQL = 被动\_级别，您[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtDpcFunc*](https://msdn.microsoft.com/library/windows/hardware/ff541683)回调函数可以创建一个或多个[工作项](using-framework-work-items.md)，使该代码将作为运行[ *EvtWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541859)回调函数。

    或者，在 KMDF 版本 1.11 及更高版本中，该驱动程序可以请求一个中断的工作项通过调用[ **WdfInterruptQueueWorkItemForIsr**](https://msdn.microsoft.com/library/windows/hardware/hh439270)。 (回想一下，驱动程序的[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数可以调用**WdfInterruptQueueWorkItemForIsr**或者[ **WdfInterruptQueueDpcForIsr**](https://msdn.microsoft.com/library/windows/hardware/ff547371)，但不可同时使用两者。)

-   如果务必要同步的驱动程序[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)并[ *EvtDpcFunc* ](https://msdn.microsoft.com/library/windows/hardware/ff541683)以及使用的回调函数其他与设备相关联的回调函数，可以设置您的驱动程序**AutomaticSerialization**成员添加到**TRUE**中的中断[ **WDF\_中断\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552347)结构和 DPC 对象[ **WDF\_DPC\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551296)结构。 或者，可以使用该驱动程序[framework 自旋锁](using-framework-locks.md#framework-spin-locks)。 (设置**AutomaticSerialization**成员添加到**TRUE**不会同步[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)回调函数其他回调函数。 使用[ **WdfInterruptSynchronize** ](https://msdn.microsoft.com/library/windows/hardware/ff547389)或[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)同步*EvtInterruptIsr*回调函数，如本主题中前面所述。)

有关同步驱动程序例程的详细信息，请参阅[基于框架的驱动程序的同步技术](synchronization-techniques-for-wdf-drivers.md)。

 

 





