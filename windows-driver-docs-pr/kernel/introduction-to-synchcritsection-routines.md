---
title: SynchCritSection 例程简介
description: SynchCritSection 例程简介
ms.assetid: 747f314a-9c7c-427f-bc23-4c6869853852
keywords:
- SynchCritSection
- 关键部分例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d4573b09243f378b9eb5f6c159404fabcd9708
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838619"
---
# <a name="introduction-to-synchcritsection-routines"></a>SynchCritSection 例程简介





*关键部分*是需要独占访问硬件资源或驱动程序数据的代码部分。 也就是说，代码不得由可以引用相同资源或数据的其他代码中断，并且一次只能有多个处理器引用资源或数据。

关键部分应限制为 Isr 和*SynchCritSection*值，并获取旋转锁。 *SynchCritSection*例程返回后，系统将释放旋转锁并降低处理器的 IRQL。

将处理器的 IRQL 提高到设备的 DIRQL 值，可防止当前处理器被中断，除非是优先级较高的设备除外。 获取旋转锁可防止其他处理器执行与该旋转锁关联的任何关键部分代码。 （此旋转锁定有时称为*中断旋转锁定*。）

设备驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)和[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)或[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程经常必须访问一些相同的[硬件资源](hardware-resources.md)（例如设备寄存器或其他与总线相关的内存）或驱动程序维护的数据作为驱动程序的ISR. 根据驱动程序的设备或设计，其调度、 [*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)、 [*ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)或计时器例程还可以访问硬件资源或驱动程序维护的数据。

若要调用任何非 ISR 关键部分，驱动程序必须使用[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)例程。 此例程接受*SynchCritSection*例程的地址作为输入，连同驱动程序定义的上下文信息和中断对象指针。 系统使用中断对象指针确定要用于*SynchCritSection*例程的 DIRQL 和旋转锁。 （驱动程序以前使用[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)函数的*旋转锁*和*SynchronizeIrql*参数提供了这些值。）

 

 




