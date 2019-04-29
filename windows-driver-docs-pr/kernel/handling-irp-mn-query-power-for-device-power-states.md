---
title: 处理设备电源状态的 IRP_MN_QUERY_POWER
description: 处理设备电源状态的 IRP_MN_QUERY_POWER
ms.assetid: 902619bc-068a-4613-b99d-78a243f7fee6
keywords:
- IRP_MN_QUERY_POWER
- 设备电源状态 WDK 内核
- 查询能耗 Irp WDK 电源管理
- power Irp WDK 内核，设备查询
- 查询能耗状态
- 队列的 Irp
- 设备查询 power Irp WDK 内核
- 调度例程 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c202c7091cc98c0371de81c49328e98d452f4d90
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392466"
---
# <a name="handling-irpmnquerypower-for-device-power-states"></a>处理 IRP\_MN\_查询\_的电源可用于设备的电源状态





设备查询能耗 IRP 查询有关单个设备的状态更改，并发送到所有设备的堆栈中的驱动程序。 指定此类 IRP **DevicePowerState**中**Power.Type** I/O 堆栈位置的成员。

驱动程序处理查询能耗 Irp，因为它们沿堆栈向下移动。

函数或筛选器驱动程序可能会失败[ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)请求以下为真：

-   设备启用了唤醒并在请求的电源状态下低于设备可以将系统唤醒从其状态。 例如，可以将系统从 D2 但不能从 D3 唤醒的设备将 D3 的失败查询，但为 D2 成功查询。

-   输入请求的状态会强制驱动程序放弃可能会丢失数据，例如打开调制解调器连接的操作。 驱动程序很少会失败查询出于此原因;在大多数情况下，应用程序处理这种情况。

失败[ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)请求，驱动程序将执行以下步骤：

1.  调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)以指示驱动程序已准备好处理 IRP 的下一个幂。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅。）

2.  设置**Irp-&gt;IoStatus.Status**为失败状态，并调用[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)，指定 IO\_否\_增量。 该驱动程序将 IRP 进一步向下设备堆栈不传递。

3.  返回的错误状态及其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

如果该驱动程序成功查询能耗 IRP，它必须开始执行任何操作或不采取任何措施阻止其成功完成的后续**IRP\_MN\_设置\_POWER**请求的查询的电源状态。

成功 IRP 的驱动程序必须准备用于查询的状态和关闭查询 IRP，传递集 power IRP，如下所示：

1.  完成任何未完成 I/O 操作。

2.  传入的 I/O 请求排队。

3.  避免从开始到指定的电源状态的转换将影响的任何其他新的活动。 但是，该驱动程序不应保存设备上下文或执行其他步骤向关闭。

4.  调用**IoCopyCurrentIrpStackLocationToNext**设置下一步低驱动程序的 IRP 堆栈位置。

5.  设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。 在中*IoCompletion*例程，调用**PoStartNextPowerIrp** （Windows Server 2003、 Windows XP 和 Windows 2000 仅） 以指示驱动程序是否准备好处理 IRP 的下一个幂。

6.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （在 Windows 7 和 Windows Vista） 或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （在 Windows Server 2003、 Windows XP 和 Windows 2000）若要将查询 IRP 传递到下一个较低的驱动程序。 无法完成 IRP。

7.  返回状态\_PENDING。 该驱动程序不得更改处的值**Irp-&gt;IoStatus.Status**。

当查询能耗 IRP 到达总线驱动程序时，总线驱动程序调用**PoStartNextPowerIrp** （Windows Server 2003、 Windows XP 和 Windows 2000 仅），并设置**Irp-&gt;IoStatus.Status**到状态\_成功如果驱动程序可以将更改为指定的电源状态，或如果不能设置失败状态。 然后，总线驱动程序调用**IoCompleteRequest**，指定 IO\_否\_增量。

在典型的设备堆栈句柄设备驱动程序查询能耗 IRP 为如下所示：

-   大多数筛选器驱动程序应只需将 IRP 传递到下一个较低的驱动程序 (请参阅[传递 Power Irp](passing-power-irps.md)) 并返回状态\_PENDING。 某些筛选器驱动程序，但是，可能首先需要执行特定于设备的任务，例如队列传入 Irp 或保存设备电源状态。

-   功能驱动程序执行特定于设备的任务 （例如，完成的挂起 I/O 请求队列的传入 I/O 请求，正在保存设备上下文，或更改设备电源） 设置*IoCompletion*例程，并将传递设备电源 IRP 到下一步低驱动程序 (请参阅[传递 Power Irp](passing-power-irps.md))。 它将返回状态\_PENDING 从其*DispatchPower*例程。

-   总线驱动程序调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776) （Windows Server 2003、 Windows XP 和 Windows 2000 仅） 以启动下一个幂 IRP。 然后完成 IRP，指定 IO\_否\_增量。 如果该驱动程序无法立即完成 IRP，则会调用[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)，将返回状态\_PENDING 从其*DispatchPower*例程，并完成 IRP 更高版本。

即使在目标设备已在查询的电源状态，每个函数或筛选器驱动程序必须排队 I/O 并将传递到下一步低驱动程序 IRP。 IRP 必须一直沿设备堆栈向下移动到总线驱动程序，它完成后，它。

处理时**IRP\_MN\_查询\_POWER**请求，驱动程序应返回从*DispatchPower*尽可能快地例程。 驱动程序必须等待中其*DispatchPower*代码处理相同的 IRP 信号的内核事件的例程。 因为 power Irp 整个系统同步的可能会发生死锁。

 

 




