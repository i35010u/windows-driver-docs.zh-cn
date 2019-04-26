---
title: SynchCritSection 例程简介
description: SynchCritSection 例程简介
ms.assetid: 747f314a-9c7c-427f-bc23-4c6869853852
keywords:
- SynchCritSection
- 关键节例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7e02b17f51039231c2a986978e1e26983590f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327237"
---
# <a name="introduction-to-synchcritsection-routines"></a>SynchCritSection 例程简介





*临界区*是需要独占访问硬件资源或驱动程序数据的代码段。 也就是说，代码不能中断的同一资源或数据，可以引用其他代码和资源或数据必须不引用由多个处理器一次。

临界区应局限于 Isr 和*SynchCritSection*值以及获取自旋锁。 之后*SynchCritSection*例程返回时，系统释放自旋锁并降低处理器的 IRQL。

引发到设备的 DIRQL 值处理器的 IRQL 防止被中断，当前处理器由优先级较高的设备除外。 获取数值调节钮锁会阻止其他处理器执行任何与该数值调节钮锁相关的关键部分代码。 (此数值调节钮锁有时称为*中断自旋锁*。)

设备驱动程序[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)并[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程经常必须访问的一些[硬件资源](hardware-resources.md)（如设备寄存器或其他总线相对内存） 或驱动程序的 ISR.作为驱动程序维护的数据 具体取决于驱动程序的设备或设计，其调度[ *AdapterControl*](https://msdn.microsoft.com/library/windows/hardware/ff540504)， [ *ControllerControl*](https://msdn.microsoft.com/library/windows/hardware/ff542049)，或计时器例程还可能会访问硬件资源或驱动程序维护的数据。

若要调用任何非 ISR 关键节，驱动程序必须使用[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)例程。 此例程接受的地址*SynchCritSection*例程作为输入，以及驱动程序定义的上下文信息并中断对象指针。 系统使用中断对象指针来确定要使用的 DIRQL 和数值调节钮锁定*SynchCritSection*例程。 (该驱动程序之前提供这些值，使用[ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)函数的*旋转锁*并*SynchronizeIrql*参数。）

 

 




