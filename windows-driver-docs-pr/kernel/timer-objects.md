---
title: 计时器对象
description: 任何驱动程序可以使用计时器驱动程序中的超时操作在 nonarbitrary 线程上下文中的对象的其他例程，或若要计划定期执行操作。
ms.assetid: A4844F19-3BEC-48C0-A5BF-E17CCEEC1601
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0d96b63cdf5d312a7edc0a760ee5d3a7dde09a85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382957"
---
# <a name="timer-objects"></a>计时器对象


任何驱动程序可以使用计时器驱动程序中的超时操作在 nonarbitrary 线程上下文中的对象的其他例程，或若要计划定期执行操作。 从 Windows 2000 开始，计时器对象基于[ **KTIMER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构均可用于与[ **KeSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)和其他**Ke*Xxx*计时器**例程。 从 Windows 8.1 开始，计时器对象基于[ **EX\_计时器**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构均可用于与[ **ExSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)和其他**Ex*Xxx*计时器**例程。 计时器对象基于**KTIMER**并**EX\_计时器**结构[内核调度程序对象](kernel-dispatcher-objects.md)计时器过期时，都已终止。 计时器超时可以是定期或一次性 （非周期性）。

本部分包含以下主题：

-   [KeXxxTimer 例程、 KTIMER 对象和 dpc 进行标记](timer-objects-and-dpcs.md)

-   [ExXxxTimer 例程和 EX\_计时器对象](exxxxtimer-routines-and-ex-timer-objects.md)

 

 




