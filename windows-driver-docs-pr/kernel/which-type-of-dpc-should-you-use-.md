---
title: 应使用哪种类型的 DPC
description: 应使用哪种类型的 DPC
ms.assetid: 7a8e6d75-5573-4a94-a895-fa2f70856807
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbbf54e942a197eda2172021cc7b7707c16a9975
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185237"
---
# <a name="which-type-of-dpc-should-you-use"></a>应使用哪种类型的 DPC？





根据驱动程序的设计，它可以具有下列任何一种：

-   用于完成所有中断驱动 i/o 操作的单个[*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)

-   一个或多个 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程的集合。

-   *DpcForIsr*和一组特定于操作的*CustomDpc*例程

驱动程序是单个 *DpcForIsr* 例程、一组 *CustomDpc* 例程还是同时具有这两者，取决于其基础设备的性质以及它必须支持的 i/o 请求集。

大多数最低级别的设备驱动程序都有一个 *DpcForIsr* 例程，用于为每个 IRP 完成 i/o 处理，需要对各自的设备执行一项或多项操作。 使用单个 *DpcForIsr* 来完成每个请求、在一次执行一个操作的设备上的中断驱动 i/o 操作相对容易。 此类驱动程序的 ISR 只需要为每个中断驱动的 i/o 操作调用 [**IoRequestDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc) 。

最低级别的驱动程序具有 *CustomDpc* 例程，除非其设备需要多个 DPC 才能完成一组不同的中断驱动 i/o 操作。

使用单个 *DpcForIsr* 在可执行并发操作的设备上完成重叠的中断驱动 i/o 操作时，可能需要仔细设计，但这可能比较困难。 除了或而不是对*DpcForIsr*进行排队外，ISR 还可以通过调用[**KeInsertQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)，将一组特定于驱动程序的*CustomDpc*例程排队。

例如，请考虑编写串行驱动程序时所涉及的一些设计挑战。 作为全双工设备的驱动程序，串行驱动程序不能依赖于在多任务系统的多处理器系统中将 Irp 排队到 *StartIo* 例程的顺序和其设备的中断顺序。 此外，串行驱动程序必须处理超时请求和异步用户生成的请求，以取消以前请求的操作、清除缓冲的数据等。

因此，串行驱动程序可以为用户模式 COM 端口应用程序请求的读取、写入、清除和等待操作维护内部队列。 它还可以维护引用计数，或对其内部队列中的 Irp 使用某些其他跟踪机制（例如一组标志）。 它的 ISR 将使用多个驱动程序分配和初始化的 DPC 对象（每个对象都与驱动程序提供的*CustomDpc*例程关联）调用**KeInsertQueueDpc** 。

 

