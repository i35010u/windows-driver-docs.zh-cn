---
title: 编写 SynchCritSection 例程
description: 编写 SynchCritSection 例程
ms.assetid: b02e230e-48f1-43dc-b5aa-368cd7b5436f
keywords:
- SynchCritSection
- 关键部分例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b6ddf7ac5b9c4808db7d06dd3a375ff3cfdaab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838292"
---
# <a name="writing-synchcritsection-routines"></a>编写 SynchCritSection 例程





驱动程序将其[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程用于以下两种基本用途：

[为 i/o 操作编程设备](programming-a-device-for-an-i-o-operation.md)

[访问共享状态信息](accessing-shared-state-information.md)

与 ISR 一样， *SynchCritSection*例程必须尽可能快地执行，在返回之前只需执行设置设备注册或更新上下文数据所需的操作。

由于[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)在其*SynchCritSection*例程运行时保存了设备驱动程序的中断自旋锁，因此在*SynchCritSection*例程返回控制权之前，不能执行驱动程序的 ISR。

对于任何收到的 IRP，设备驱动程序应尽可能多地在其调度例程（或可能是[设备专用的线程](device-dedicated-threads.md)）的 irql 被动\_级别执行 i/o 处理，或在[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程中以 irql 调度\_级别和 DPC 例程。

有关如何同步关键节的其他信息，请参阅[使用自旋锁：一个示例](using-spin-locks--an-example.md)。

 

 




