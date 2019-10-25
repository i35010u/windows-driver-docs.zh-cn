---
title: DPC 简介
description: DPC 简介
ms.assetid: 10e8d0e7-c04a-4dca-853c-74c911f59341
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a71650b6943d36e77daaf19244f086eb0fd882f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828216"
---
# <a name="introduction-to-dpcs"></a>DPC 简介





具有 ISR 的任何驱动程序通常还至少具有一个[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)或[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程来完成对中断驱动的 i/o 操作的处理。 典型的最低级别驱动程序的*DpcForIsr*或*CustomDpc*例程会执行以下操作：

-   处理 ISR 开始处理的 i/o 操作。

-   取消排队下一个 IRP，以便驱动程序可以开始处理。

-   完成当前 IRP （如果可能）。

有时无法完成当前 IRP，因为需要几个数据传输，或者检测到可恢复的错误。 在这些情况下， *DpcForIsr*或*CustomDpc*例程通常会将设备 reprograms 为另一次传输或重试上一操作。

在*DpcForIsr*或*CustomDpc*例程的任意 DPC 上下文中都调用了 IRQL 调度\_级别。 在调度\_级别运行会限制*DpcForIsr*或*CustomDpc*例程可以调用的一组支持例程。 有关详细信息，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

DPC 对象和 Dpc 还可与计时器一起使用。 有关详细信息，请参阅[Timer 对象和 dpc](timer-objects-and-dpcs.md)。

 

 




