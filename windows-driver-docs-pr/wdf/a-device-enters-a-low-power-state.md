---
title: 在设备进入低功耗状态
description: 在设备进入低功耗状态
ms.assetid: 07d7c460-4316-40a9-b502-f7c1bd1182c2
keywords:
- 电源管理 WDK KMDF，低功耗状态
- 低功耗状态 WDK KMDF
- 电源状态 WDK KMDF
- 设备电源状态 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 空闲关闭 WDK KMDF
- 电源管理 WDK KMDF、 空闲关机
- 系统睡眠状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2047a746c6366da0ad7527b73bb9a7f14b76cccf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554278"
---
# <a name="a-device-enters-a-low-power-state"></a>在设备进入低功耗状态


设备会使其工作 (D0) 状态，并进入低功耗状态，如果发生以下情况之一：

-   设备处于空闲状态 （的，没有访问） 并能够进入低能耗空闲状态，而系统仍然处于其工作 (S0) 状态。

-   系统的电源状态已从其工作 (S0) 状态更改为低功耗状态。 (驱动程序可以调用[ **WdfDeviceGetSystemPowerAction** ](https://msdn.microsoft.com/library/windows/hardware/ff546022)以确定系统的电源状态更改的原因。)

对于每个函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，一个驱动程序时，开始驱动程序堆栈中最高的驱动程序：

1.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)回调函数。

2.  该框架将停止所有驱动程序的电源管理的 I/O 队列并调用其[ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788)回调函数 （如果存在）。

3.  如果该驱动程序是设备的电源策略所有者，框架将调用其[ *EvtDeviceArmWakeFromS0*](https://msdn.microsoft.com/library/windows/hardware/ff540843)， [ *EvtDeviceArmWakeFromSx* ](https://msdn.microsoft.com/library/windows/hardware/ff540844)，或[ *EvtDeviceArmWakeFromSxWithReason* ](https://msdn.microsoft.com/library/windows/hardware/ff540846)回调函数。

4.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)， [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)，并[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)回调函数 （如果存在） 用于创建每个 DMA 通道。

5.  框架将调用的驱动程序[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)回调函数 （如果存在），然后它调用的驱动程序[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)回调函数，（如果存在） 为每个中断，使驱动程序可以禁用设备中断。

6.  框架将调用的驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数 （如果存在）。

总线驱动程序是最后调用堆栈中的驱动程序。 当框架将调用总线驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数，则回调函数会将设备 （在总线的子设备） 的电源状态设置为低功耗状态。 该框架指定 D3 低功耗状态，除非电源策略所有者已指定不同的低功耗状态。

 

 





