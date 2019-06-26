---
title: DPC 简介
description: DPC 简介
ms.assetid: 10e8d0e7-c04a-4dca-853c-74c911f59341
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0461fc51f4cc7498a87c8ae85567ac61f2d3e383
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369767"
---
# <a name="introduction-to-dpcs"></a>DPC 简介





通常具有 ISR 任何驱动程序还具有至少一个[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)或[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)的完成处理例程中断驱动 I/O 操作。 典型的最低级别驱动*DpcForIsr*或*CustomDpc*例程执行以下操作：

-   处理 ISR 开始处理的 I/O 操作完成。

-   通过下一步 IRP 取消排队，以便该驱动程序可以开始处理它。

-   如有可能完成当前的 IRP。

有时无法完成当前的 IRP，因为多个数据传输都是必需的或者检测到可恢复的错误。 在这些情况下， *DpcForIsr*或*CustomDpc*例程通常 reprograms 设备的另一个传输或最后一次操作的重试。

一个*DpcForIsr*或*CustomDpc* IRQL 调度在任意 DPC 上下文中调用例程\_级别。 运行在调度\_级别限制集的支持例程*DpcForIsr*或*CustomDpc*例程可以调用。 请参阅[管理硬件优先级](managing-hardware-priorities.md)有关详细信息。

DPC 对象和 dpc 进行标记还可以使用计时器。 有关详细信息，请参阅[计时器对象和 dpc 进行标记](timer-objects-and-dpcs.md)。

 

 




