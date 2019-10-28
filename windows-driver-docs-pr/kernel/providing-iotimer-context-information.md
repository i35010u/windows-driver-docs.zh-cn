---
title: 提供 IoTimer 上下文信息
description: 提供 IoTimer 上下文信息
ms.assetid: a92a7c3d-1602-430b-8ae1-c79bfc9ac7f9
keywords:
- IoTimer
- IoInitializeTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b52cdcd597811f2eb099992df30a41611396b9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838484"
---
# <a name="providing-iotimer-context-information"></a>提供 IoTimer 上下文信息





传递给[**IoInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)的*上下文*指针会标识一个上下文区域，其中其他驱动程序例程和[*IoTimer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_timer_routine)例程本身都可以维护有关计时操作的状态。 每次调用*IoTimer*例程时，i/o 管理器都将传递*上下文*指针。

由于*IoTimer*例程是在 IRQL = 调度\_级别运行的，因此其上下文区域必须在常驻的系统空间内存中。 大多数具有*IoTimer*例程的驱动程序使用关联设备对象的[设备扩展](device-extensions.md)作为*上下文*可访问的区域，但如果驱动程序使用[控制器对象](using-controller-objects.md)或驱动程序分配的非分页池中。

对于*IoTimer * * * 例程的上下文区域* **，请遵循以下准则**：*

-   如果*IoTimer*例程与驱动程序的 ISR 共享其上下文区域，则它必须使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)来调用[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程，该例程通过多处理器安全的方式访问上下文区。 有关详细信息，请参阅[使用关键部分](using-critical-sections.md)。

-   如果*IoTimer*例程不与 ISR 共享其上下文区域，而是与另一个驱动程序例程共享它，则驱动程序必须使用已初始化的执行单元旋转锁来保护共享上下文区域，以便访问多处理器安全的方式。 有关详细信息，请参阅[自旋锁](spin-locks.md)。

 

 




