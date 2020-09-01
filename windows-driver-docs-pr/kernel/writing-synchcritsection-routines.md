---
title: 编写 SynchCritSection 例程
description: 编写 SynchCritSection 例程
ms.assetid: b02e230e-48f1-43dc-b5aa-368cd7b5436f
keywords:
- SynchCritSection
- 关键部分例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c93375d843a37aaa542a85ca3fed5d35fafeda87
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188831"
---
# <a name="writing-synchcritsection-routines"></a>编写 SynchCritSection 例程





驱动程序将其 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程用于以下两种基本用途：

[为 i/o 操作编程设备](programming-a-device-for-an-i-o-operation.md)

[访问共享状态信息](accessing-shared-state-information.md)

与 ISR 一样， *SynchCritSection* 例程必须尽可能快地执行，在返回之前只需执行设置设备注册或更新上下文数据所需的操作。

由于 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 在其 *SynchCritSection* 例程运行时保存了设备驱动程序的中断自旋锁，因此在 *SynchCritSection* 例程返回控制权之前，不能执行驱动程序的 ISR。

对于任何收到的 IRP，设备驱动程序都应尽可能多地执行 i/o 处理操作， \_ 其调度 (例程中的 StartIo 或可能是[设备专用线程](device-dedicated-threads.md)) ，或者在 \_ 其[*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程和 DPC 例程中处于 irql 调度级别。

有关如何同步关键节的其他信息，请参阅 [使用自旋锁：一个示例](using-spin-locks--an-example.md)。

 

