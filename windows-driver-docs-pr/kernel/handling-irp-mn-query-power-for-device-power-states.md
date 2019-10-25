---
title: 处理设备电源状态的 IRP_MN_QUERY_POWER
description: 处理设备电源状态的 IRP_MN_QUERY_POWER
ms.assetid: 902619bc-068a-4613-b99d-78a243f7fee6
keywords:
- IRP_MN_QUERY_POWER
- 设备电源状态 WDK 内核
- 查询-power Irp WDK 电源管理
- power Irp WDK 内核，设备查询
- 查询电源状态
- 队列 Irp
- 设备查询电源 Irp WDK 内核
- 调度例程 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d2e30a646d898d44d234683e9ca6bd6abede35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836500"
---
# <a name="handling-irp_mn_query_power-for-device-power-states"></a>处理 IRP\_MN\_查询\_设备电源状态的电源





设备查询-power IRP 会查询单个设备的状态更改，并将其发送到设备堆栈中的所有驱动程序。 此类 IRP 在 i/o 堆栈位置的 DevicePowerState**成员中**指定了 。

驱动程序在传递堆栈时处理查询电源 Irp。

如果满足以下任一条件，则函数或筛选器驱动程序可能会导致[**IRP\_MN\_查询\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)请求失败：

-   设备启用了唤醒，并且请求的电源状态低于设备可用于唤醒系统的状态。 例如，可以从 D2 而不是 D3 唤醒系统的设备将无法查询 D3，但会成功查询 D2。

-   进入请求状态将强制驱动程序放弃会丢失数据的操作，如打开的调制解调器连接。 出于此原因，驱动程序很少导致查询失败;在大多数情况下，应用程序会处理这种情况。

若要使[**IRP\_MN\_QUERY\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) request，驱动程序需要执行以下步骤：

1.  调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) ，以指示驱动程序已准备好处理下一个电源 IRP。 （仅限 windows Server 2003、Windows XP 和 Windows 2000。）

2.  将**Irp&gt;IoStatus**设置为失败状态，并调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)，同时指定 IO\_无\_增量。 驱动程序不会沿着设备堆栈进一步向下传递 IRP。

3.  从其[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回错误状态。

如果驱动程序成功执行了查询-power IRP，则它不能启动任何操作，也不采取任何其他措施来阻止成功完成后续**IRP\_MN\_将\_电源请求设置**为所查询的电源状态。

成功完成 IRP 的驱动程序必须为用于查询状态的集电源 IRP 做好准备，并按如下所示向下传递查询 IRP：

1.  完成所有未完成的 i/o 操作。

2.  为传入 i/o 请求排队。

3.  避免启动会干扰转换到指定电源状态的任何其他新活动。 但是，驱动程序不应保存设备上下文或执行其他步骤来关闭。

4.  调用**IoCopyCurrentIrpStackLocationToNext**以设置下一个较低驱动程序的 IRP 堆栈位置。

5.  设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 在*IoCompletion*例程中，调用**PoStartNextPowerIrp** （仅限 Windows SERVER 2003、windows XP 和 windows 2000），以指示驱动程序准备好处理下一个电源 IRP。

6.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （在 windows 7 和 windows Vista 中）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （在 Windows SERVER 2003、windows XP 和 windows 2000 中），将 query IRP 传递到下一个较低版本的驱动程序。 不要完成 IRP。

7.  返回状态\_挂起。 驱动程序不得更改**Irp&gt;IoStatus**的值。

当查询-power IRP 达到总线驱动程序时，bus 驱动程序将调用**PoStartNextPowerIrp** （仅限 windows Server 2003、windows XP 和 windows 2000），并将**IRP&gt;IoStatus**状态设置\_为 "成功" （如果驱动程序可以更改为）指定的电源状态，如果不能，则设置失败状态。 然后，总线驱动程序调用**IoCompleteRequest**，指定 IO\_没有\_增量。

典型设备堆栈中的驱动程序处理设备查询-power IRP，如下所示：

-   大多数筛选器驱动程序只需将 IRP 传递到下一个较低的驱动程序（请参阅[通过电源 irp](passing-power-irps.md)）并返回状态\_挂起。 但是，某些筛选器驱动程序可能首先需要执行特定于设备的任务，例如将传入的 Irp 排队或保存设备电源状态。

-   函数驱动程序执行特定于设备的任务（例如，完成挂起的 i/o 请求、排队传入 i/o 请求、保存设备上下文或更改设备电源）、设置*IoCompletion*例程，并将设备电源 IRP 传递到下一个较低的驱动程序（请参阅[通过电源 irp](passing-power-irps.md)）。 它从*DispatchPower*例程返回状态\_"挂起"。

-   总线驱动程序调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) （仅限 windows Server 2003、windows XP 和 windows 2000）来启动下一个 power IRP。 然后，它完成 IRP，指定 IO\_没有\_增量。 如果驱动程序无法立即完成 IRP，它将调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，并从其*DISPATCHPOWER*例程返回状态\_"挂起"，并在以后完成 irp。

即使目标设备已处于查询的电源状态，每个函数或筛选器驱动程序也必须将 i/o 排队，并将 IRP 向下传递到下一个较低的驱动程序。 IRP 必须按设备堆栈向下移动到总线驱动程序，这将完成该过程。

处理**IRP\_MN\_QUERY\_POWER** request 时，驱动程序应尽快从*DispatchPower*例程返回。 对于由处理同一 IRP 的代码发出信号的内核事件，驱动程序不得在其*DispatchPower*例程中等待。 由于 power Irp 在整个系统中同步，因此可能会发生死锁。

 

 




