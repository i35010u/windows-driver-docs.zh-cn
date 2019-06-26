---
title: 编写 SynchCritSection 例程
description: 编写 SynchCritSection 例程
ms.assetid: b02e230e-48f1-43dc-b5aa-368cd7b5436f
keywords:
- SynchCritSection
- 关键节例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0599e3160188c8f9267132e5afe916c6447d7fe5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374105"
---
# <a name="writing-synchcritsection-routines"></a>编写 SynchCritSection 例程





驱动程序使用其[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)例程的两个基本目的之一：

[编程的 I/O 操作的设备](programming-a-device-for-an-i-o-operation.md)

[访问共享的状态信息](accessing-shared-state-information.md)

喜欢 ISR *SynchCritSection*例程必须尽快，只是需要设置设备注册或更新上下文数据，在返回之前执行。

因为[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)持有设备驱动程序的中断自旋锁时其*SynchCritSection*日常运行时，驱动程序的 ISR 之前无法执行*SynchCritSection*例程将返回控制。

对于任何接收 IRP，设备驱动程序应执行太多 I/O 处理尽可能在 IRQL 被动\_级别在其调度例程 (或可能[设备专用线程](device-dedicated-threads.md))，或在 IRQL 调度\_级别中其[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程和 DPC 例程。

为了解更多信息同步临界区，请参阅[使用旋转锁：示例](using-spin-locks--an-example.md)。

 

 




