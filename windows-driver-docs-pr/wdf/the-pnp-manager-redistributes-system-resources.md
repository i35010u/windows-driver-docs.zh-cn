---
title: PnP 管理器重新分发系统资源
description: PnP 管理器重新分发系统资源
ms.assetid: fc88ae0a-5b78-4292-a101-29d2fc383555
keywords:
- PnP WDK KMDF，重新分发的资源
- 插 WDK KMDF，重新分发的资源
- 资源重新分发 WDK KMDF
- 重新分发资源 WDK KMDF
- 电源关闭序列 WDK KMDF
- 强化序列 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d0d32b15026e06fb741a36e6dd87f122e892d0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377413"
---
# <a name="the-pnp-manager-redistributes-system-resources"></a>PnP 管理器重新分发系统资源


如果用户将设备添加到系统，以及设备需要即插即用的管理员已分配给另一台设备的系统资源，即插即用管理器将尝试重新分配资源。

在此过程中，即插即用管理器停止设备并获取它们超出其工作 (D0) 状态。 它然后提供了新的资源列表到设备，以便它们可以重新启动，请使用新的资源。

在重新分发的资源，即插即用管理器不会更改设备的资源分配，如果一个设备的驱动程序具有：

-   名为[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)和特殊文件是在设备上打开。

-   名为[ **WdfDeviceSetStaticStopRemove**](https://msdn.microsoft.com/library/windows/hardware/ff546915)。

-   提供[ *EvtDeviceQueryStop* ](https://msdn.microsoft.com/library/windows/hardware/ff540885)回调函数和回调函数已禁止重新分配。

### <a name="power-down-sequence"></a>电源关闭序列

对于每个函数和筛选器驱动程序支持设备正在停止，框架将执行以下操作，在序列中，一个驱动程序时，开始驱动程序堆栈中最高的驱动程序：

1.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoSuspend* ](https://msdn.microsoft.com/library/windows/hardware/ff540907)回调函数。

2.  该框架将停止所有设备的电源管理的 I/O 队列。

3.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerSelfManagedIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541677)， [ *EvtDmaEnablerFlush* ](https://msdn.microsoft.com/library/windows/hardware/ff541655)，并[ *EvtDmaEnablerDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff540927)创建每个 DMA 通道的回调函数。

4.  调用的驱动程序[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)并[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)回调函数 （如果存在）因此，该驱动程序可以禁用设备中断。

5.  框架将调用的驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数 （如果存在）。

6.  框架将调用的驱动程序[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)传递的即插即用的管理员分配给设备的硬件资源的列表的回调函数 （如果存在）。

总线驱动程序堆栈中的最低驱动程序，最后调用。 当框架将调用总线驱动程序[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数，它将传递一个句柄到表示设备的 PDO 的 framework 设备对象和一个*TargetState*的值**WdfPowerDeviceD3Final**。 总线驱动程序可以控制当框架将调用其[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)通过调用回调函数[ **WdfDeviceInitSetReleaseHardwareOrderOnFailure**](https://msdn.microsoft.com/library/windows/hardware/hh706196)。

### <a name="power-up-sequence"></a>强化序列

调用的第一个驱动程序是总线驱动程序。 当框架将调用总线驱动程序[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)的回调函数的回调函数将设备 （在总线的子设备） 还原到其工作 (D0) 状态。

对于每个函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，使用驱动程序的最低驱动程序堆栈中启动一个时，驱动程序：

1.  框架将调用的驱动程序[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数 （如果存在），同时传入的即插即用的管理员分配给设备的硬件资源的列表。

2.  框架将调用的驱动程序[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)回调函数 （如果存在）。

3.  框架将调用的驱动程序[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)并[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)回调函数 （如果存在），以便该驱动程序可以启用设备的中断。

4.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerFill*](https://msdn.microsoft.com/library/windows/hardware/ff540932)， [ *EvtDmaEnablerEnable*](https://msdn.microsoft.com/library/windows/hardware/ff540929)，和[ *EvtDmaEnablerSelfManagedIoStart* ](https://msdn.microsoft.com/library/windows/hardware/ff541663)创建每个 DMA 通道的回调函数。

5.  框架将调用的驱动程序[ *EvtChildListScanForChildren* ](https://msdn.microsoft.com/library/windows/hardware/ff540838)回调函数 （如果存在）。

6.  该框架将重新启动的所有设备的电源管理的 I/O 队列。

7.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoRestart* ](https://msdn.microsoft.com/library/windows/hardware/ff540905)回调函数。

 

 





