---
title: 设备回到工作状态
description: 设备回到工作状态
ms.assetid: 0a5bdaf5-ed9e-44d0-bc8a-876ceb342520
keywords:
- 设备电源状态 WDK KMDF
- 工作状态 WDK KMDF
- 电源状态 WDK KMDF
- 系统唤醒 WDK KMDF
- 电源管理 WDK KMDF，唤醒功能
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce525cafebccd00971426e0ebfdcf7ea5cd58287
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342142"
---
# <a name="a-device-returns-to-its-working-state"></a>设备回到工作状态


如果发生下列其中一项处于低功耗状态的设备将恢复工作状态：

-   设备检测到的外部事件，并触发其总线上的唤醒信号。 检测到唤醒信号调用总线驱动程序[ **WdfDeviceIndicateWakeStatus**](https://msdn.microsoft.com/library/windows/hardware/ff546025)。 因此，框架将调用总线驱动程序[ *EvtDeviceDisableWakeAtBus* ](https://msdn.microsoft.com/library/windows/hardware/ff540858)回调函数。

-   设备处于空闲状态，并将驱动程序调用[ **WdfDeviceStopIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546921)。

-   系统的电源状态已从低功耗状态更改为其工作 (S0) 状态。

在每种情况下，框架将调用总线驱动程序[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)回调函数，然后将设备 （在总线的子设备） 还原到其工作 (D0) 状态。

对于每个函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，使用驱动程序的最低驱动程序堆栈中启动一个时，驱动程序：

1.  框架将调用的驱动程序[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)回调函数 （如果存在）。

2.  框架将调用的驱动程序[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)回调函数 （如果存在） 为每个中断，然后它调用的驱动程序[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)回调函数 （如果存在），以便该驱动程序可以启用设备中断。

3.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerFill*](https://msdn.microsoft.com/library/windows/hardware/ff540932)， [ *EvtDmaEnablerEnable*](https://msdn.microsoft.com/library/windows/hardware/ff540929)，和[ *EvtDmaEnablerSelfManagedIoStart* ](https://msdn.microsoft.com/library/windows/hardware/ff541663)回调函数 （如果存在） 用于创建每个 DMA 通道。

4.  如果该驱动程序是设备的电源策略所有者，框架将调用其[ *EvtDeviceDisarmWakeFromS0* ](https://msdn.microsoft.com/library/windows/hardware/ff540860)或[ *EvtDeviceDisarmWakeFromSx* ](https://msdn.microsoft.com/library/windows/hardware/ff540862)回调函数。

5.  框架将调用的驱动程序[ *EvtChildListScanForChildren* ](https://msdn.microsoft.com/library/windows/hardware/ff540838)回调函数 （如果存在）。

6.  Framework 重新启动所有驱动程序的电源管理的 I/O 队列并调用其[ *EvtIoResume* ](https://msdn.microsoft.com/library/windows/hardware/ff541779)回调函数 （如有必要）。

7.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff540905)回调函数。

 

 





