---
title: 计时器对象
description: 任何驱动程序都可以使用 nonarbitrary 线程上下文内的 timer 对象执行驱动程序的其他例程中的超时操作，或计划定期执行的操作。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0d89558f29d6fa221e0f516706283c29635d4056
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814265"
---
# <a name="timer-objects"></a>计时器对象


任何驱动程序都可以使用 nonarbitrary 线程上下文内的 timer 对象执行驱动程序的其他例程中的超时操作，或计划定期执行的操作。 从 Windows 2000 开始，可以将基于 [**KTIMER**](./eprocess.md) 结构的计时器对象与 [**KeSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer) 和其他 **Ke *Xxx* 计时器** 例程一起使用。 从 Windows 8.1 开始，基于 [**EX \_ 计时器**](./eprocess.md) 结构的计时器对象可以与 [**ExSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer) 和其他 **EX *Xxx* 计时器** 例程一起使用。 基于 **KTIMER** 和 **EX \_ 计时器** 结构的计时器对象是在计时器过期时发出信号的 [内核调度程序对象](./introduction-to-kernel-dispatcher-objects.md) 。 计时器过期时间可以是定期的，也可以是一 (非周期性) 。

本节包含下列主题：

-   [KeXxxTimer 例程、KTIMER 对象和 DPC](timer-objects-and-dpcs.md)

-   [ExXxxTimer 例程和 EX \_ 计时器对象](exxxxtimer-routines-and-ex-timer-objects.md)

 

