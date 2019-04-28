---
title: 处理设备电源状态的 IRP_MN_SET_POWER
description: 处理设备电源状态的 IRP_MN_SET_POWER
ms.assetid: b4a19995-7933-41f7-b951-15ce0e4627da
keywords:
- IRP_MN_SET_POWER
- 设备电源状态 WDK 内核
- 设置 power Irp WDK 内核
- DispatchPower 例程
- 将 Irp 传递下设备堆栈 WDK
- 设备设置 power Irp WDK 的内核
- power Irp WDK 内核，设备更改
- 调度例程 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f80deda87b323aea0d72b09ec5f2c4af319d3186
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350030"
---
# <a name="handling-irpmnsetpower-for-device-power-states"></a>处理 IRP\_MN\_设置\_的电源可用于设备的电源状态





一组 power IRP 请求用于单个设备的状态更改和设备发送到堆栈中的所有驱动程序的设备。 指定此类 IRP **DevicePowerState**中**Power.Type** I/O 堆栈位置的成员。

驱动程序处理电源关闭 Irp，如它们沿堆栈向下移动。 有关强化 Irp，驱动程序集[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程作为 Irp 沿堆栈上，向下移动，然后处理在 Irp *IoCompletion*作为 Irp 例程返回旅行堆栈上。 在典型的设备堆栈句柄设备驱动程序集 power IRP 为如下所示：

-   大多数筛选器驱动程序应只需调用[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)，将 IRP 传递给下一个较低驱动程序 (请参阅[传递 Power Irp](passing-power-irps.md))，并返回状态\_从挂起[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 某些筛选器驱动程序，但是，可能首先需要执行特定于设备的任务，例如队列传入 Irp 或保存设备电源状态。

-   功能驱动程序调用**IoMarkIrpPending**、 执行特定于设备的任务 （如完成的挂起 I/O 请求队列的传入 I/O 请求，正在保存设备上下文，或更改设备电源）、 设置*IoCompletion*例程，如有必要，并将设备电源 IRP 传递到下一个较低的驱动程序 (请参阅[传递 Power Irp](passing-power-irps.md))。 它将返回状态\_PENDING 从其*DispatchPower*例程。

-   总线驱动程序如果能够这样做的更改设备电源，然后调用[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)通知电源管理器的新设备电源状态。 在 Windows Server 2003、 Windows XP 和 Windows 2000 仅，驱动程序还必须调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)后它会设置电源状态开始下一个幂 IRP。 该驱动程序，然后完成 IRP，指定 IO\_否\_增量。 如果该驱动程序无法立即完成 IRP，则会调用[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)，将返回状态\_PENDING 从其*DispatchPower*例程，并完成 IRP 更高版本。

即使目标设备已在请求的电源状态，每个函数或筛选器驱动程序必须将传递到下一步低驱动程序 IRP。 每个集 power IRP 必须一直沿设备堆栈向下移动到总线驱动程序，它完成后，它。

位于上方总线驱动程序的函数和筛选器驱动程序不得失败设备集电源 IRP。 总线驱动程序可能会失败设备强化 IRP 如果删除该设备或正被删除。

驱动程序堆栈中的每个驱动程序 （函数、 筛选和总线驱动程序） 必须调用[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)以通知其相应的设备对象的电源状态更改的电源管理器。

喜欢与设备强化和电源关闭，将会调用其他驱动程序任务**PoSetPowerState**必须出现在设备上 （如果新的状态是 D0） 为提供的支持后或之前设备关闭 （如果新的状态是任何其他状态） 为提供的支持。

每个驱动程序应跟踪的其设备的电源状态。 电源管理器不提供此信息来驱动程序。

在处理[ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)设备电源状态，驱动程序的请求应返回从*DispatchPower*尽可能快地例程。 驱动程序必须等待中其*DispatchPower*代码处理相同的 IRP 信号的内核事件的例程。 因为 power Irp 整个系统同步的可能会发生死锁。

若要确保最高级别的系统性能，尤其是对于多媒体应用程序，驱动程序应执行耗时级别操作中断请求 (IRQL) 等于被动\_级别。 执行操作在 IRQL = 被动\_级别，可以使用驱动程序[专用线程](device-dedicated-threads.md)或[系统工作线程](system-worker-threads.md)。 有关优化多媒体平台的驱动程序性能的指南，请参阅[流式处理媒体设备设计指南](https://msdn.microsoft.com/library/windows/hardware/ff568270)。

驱动程序必须采取来处理 power IRP 的确切步骤取决于打开设备电源，如以下各节中所述：

[处理设备电源关闭 Irp](handling-device-power-down-irps.md)

[处理设备强化 Irp](handling-device-power-up-irps.md)

 

 




