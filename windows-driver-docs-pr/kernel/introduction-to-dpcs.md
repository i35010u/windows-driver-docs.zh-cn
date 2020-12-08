---
title: DPC 简介
description: DPC 简介
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1297a0e916a4c8f2fabcdc654e8500fa0003c40
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838771"
---
# <a name="introduction-to-dpcs"></a>DPC 简介





具有 ISR 的任何驱动程序通常还至少具有一个 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程来完成对中断驱动的 i/o 操作的处理。 典型的最低级别驱动程序的 *DpcForIsr* 或 *CustomDpc* 例程会执行以下操作：

-   处理 ISR 开始处理的 i/o 操作。

-   取消排队下一个 IRP，以便驱动程序可以开始处理。

-   完成当前 IRP （如果可能）。

有时无法完成当前 IRP，因为需要几个数据传输，或者检测到可恢复的错误。 在这些情况下， *DpcForIsr* 或 *CustomDpc* 例程通常会将设备 reprograms 为另一次传输或重试上一操作。

*DpcForIsr* 或 *CustomDpc* 例程在具有 IRQL 调度级别的任意 DPC 上下文中调用 \_ 。 在调度 \_ 级别运行会限制 *DpcForIsr* 或 *CustomDpc* 例程可以调用的支持例程集。 有关详细信息，请参阅 [管理硬件优先级](managing-hardware-priorities.md) 。

DPC 对象和 Dpc 还可与计时器一起使用。 有关详细信息，请参阅 [Timer 对象和 dpc](timer-objects-and-dpcs.md)。

 

