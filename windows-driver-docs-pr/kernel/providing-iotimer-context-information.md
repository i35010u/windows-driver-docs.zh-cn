---
title: 提供 IoTimer 上下文信息
description: 提供 IoTimer 上下文信息
ms.assetid: a92a7c3d-1602-430b-8ae1-c79bfc9ac7f9
keywords:
- IoTimer
- IoInitializeTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3681d2b533432265c245dae9772b9d01f71741b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189509"
---
# <a name="providing-iotimer-context-information"></a>提供 IoTimer 上下文信息





传递给[**IoInitializeTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)的*上下文*指针会标识一个上下文区域，其中其他驱动程序例程和[*IoTimer*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程本身都可以维护有关计时操作的状态。 每次调用*IoTimer*例程时，i/o 管理器都将传递*上下文*指针。

由于 *IoTimer* 例程是在 IRQL = 调度级别运行的 \_ ，因此其上下文区域必须在常驻的系统空间内存中。 大多数具有 *IoTimer* 例程的驱动程序使用关联设备对象的 [设备扩展](device-extensions.md) 作为 *上下文*可访问的区域，但如果驱动程序使用 [控制器对象](./introduction-to-controller-objects.md) 或由驱动程序分配的非分页池，则上下文可以位于控制器扩展中。

对于*IoTimer * * * 例程的上下文区域* **，请遵循以下准则**：*

-   如果 *IoTimer* 例程与驱动程序的 ISR 共享其上下文区域，则它必须使用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 来调用 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程，该例程通过多处理器安全的方式访问上下文区。 有关详细信息，请参阅 [使用关键部分](using-critical-sections.md)。

-   如果 *IoTimer* 例程不与 ISR 共享其上下文区域，而是与另一个驱动程序例程共享它，则驱动程序必须使用已初始化的执行单元旋转锁来保护共享上下文区域，以便以多处理器安全的方式访问上下文信息。 有关详细信息，请参阅 [自旋锁](./introduction-to-spin-locks.md)。

 

