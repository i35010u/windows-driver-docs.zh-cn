---
title: 计时器对象
description: 任何驱动程序都可以使用 nonarbitrary 线程上下文内的 timer 对象执行驱动程序的其他例程中的超时操作，或计划定期执行的操作。
ms.assetid: A4844F19-3BEC-48C0-A5BF-E17CCEEC1601
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b7b9bfa2d8fe9503d1c96a46d0df0b5e5a78d42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836118"
---
# <a name="timer-objects"></a>计时器对象


任何驱动程序都可以使用 nonarbitrary 线程上下文内的 timer 对象执行驱动程序的其他例程中的超时操作，或计划定期执行的操作。 从 Windows 2000 开始，可以将基于[**KTIMER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构的计时器对象与[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)和其他**Ke*Xxx*计时器**例程一起使用。 从 Windows 8.1 开始，基于[**EX\_定时器**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构的计时器对象可用于[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)和其他**EX*Xxx*计时器**例程。 基于**KTIMER**和**EX\_定时器**结构的计时器对象是在计时器过期时发出信号的[内核调度程序对象](kernel-dispatcher-objects.md)。 计时器过期时间可以是定期或一次拍摄（非周期性）。

本部分包含以下主题：

-   [KeXxxTimer 例程、KTIMER 对象和 Dpc](timer-objects-and-dpcs.md)

-   [ExXxxTimer 例程和 EX\_计时器对象](exxxxtimer-routines-and-ex-timer-objects.md)

 

 




