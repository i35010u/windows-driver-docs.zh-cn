---
title: 处理设备强化 Irp
description: 处理设备强化 Irp
ms.assetid: 8fcfd324-97f9-4fd0-8fa1-87685c6b5ec3
keywords:
- 设置 power Irp WDK 内核
- 设备设置 power Irp WDK 的内核
- power Irp WDK 内核，设备更改
- 强化 Irp WDK 内核
- 启动 power management WDK 内核
- 还原 power WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: db661a11878c38fbac46d1f972afaf3ee6969900
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524128"
---
# <a name="handling-device-power-up-irps"></a>处理设备强化 Irp





设备指定强化 Irp [ **IRP\_MN\_设置\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)和要求更高能力比当前设备电源状态的设备电源状态。 通常情况下，强化 IRP 指定设备工作状态**PowerDeviceD0**。

按基础总线驱动程序对于设备，然后按在堆栈中向上返回将每个连续驱动程序，必须首先处理设备保持开机状态的请求。

下图显示所涉及步骤中处理强化 IRP。

![说明处理设备强化请求的关系图](images/devd0.png)

在处理时**IRP\_MN\_设置\_POWER**函数或筛选器驱动程序必须为强化，请求：

-   调用[ **IoAcquireRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548204)若要确保该驱动程序不接收[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)时处理强化 IRP 的请求。

    如果**IoAcquireRemoveLock**返回失败状态，该驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成 IRP，然后返回失败状态。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，该驱动程序应调用**IoCompleteRequest**若要完成 IRP，然后调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)启动接下来 power IRP，，然后返回失败状态。

-   调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)将挂起的 IRP 标记。

-   调用[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)设置 IRP 堆栈位置。 驱动程序不能调用**IoSkipCurrentIrpStackLocation**如果它设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。

-   调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)若要设置增益道具*IoCompletion*例程。

    该驱动程序时处理设备强化 IRP，应设置*IoCompletion*例程，以还原上下文、 释放删除锁，并执行其他所需的任务完成 IRP 后和在设备接通电源。 该驱动程序不应还原上下文之前 IRP 已经完成。 有关详细信息，请参阅[设备电源 Irp 的 IoCompletion 例程](iocompletion-routines-for-device-power-irps.md)。

-   调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （在 Windows 7 和 Windows Vista） 或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （Windows Server 2003、 Windows XP 和 Windows 2000） 到将 IRP 传递给下一个较低驱动程序。 IRP 必须一直沿设备堆栈向下移动到总线驱动程序。 只有总线驱动程序能够完成 IRP。

-   返回状态\_PENDING。

当总线驱动程序接收 IRP 时，则它应首先检查以确保该设备仍然存在，尚未删除或替换处于睡眠状态时。 如果设备已不再存在，总线驱动程序应调用[ **IoInvalidateDeviceRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff549353)父设备通知设备已消失的插管理器上。 在这种情况下，总线驱动程序可能会失败设备强化 IRP。

如果该设备仍然存在，总线驱动程序然后执行将设备恢复为操作的条件，调用所需的任务[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)通知电源管理器的新设备电源状态，并完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343))。 如果驱动程序让设备进入休眠状态，而排队等待 I/O 或设备要求浪涌能力，总线驱动程序将适用于设备的电源。 否则，总线驱动程序电源后立即应用它必须与设备通信。

若要实现与关闭电源、 standby 和休眠状态的快速启动时间的最佳实践的列表，请参阅[提高系统启动性能](improving-system-startup-performance.md)。

 

 




