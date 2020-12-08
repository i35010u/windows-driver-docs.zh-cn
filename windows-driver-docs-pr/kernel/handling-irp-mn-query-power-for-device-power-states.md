---
title: 处理设备电源状态的 IRP_MN_QUERY_POWER
description: 处理设备电源状态的 IRP_MN_QUERY_POWER
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
ms.openlocfilehash: 6a4ffec7c273698d7f733c768384c5fb308d2e90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836405"
---
# <a name="handling-irp_mn_query_power-for-device-power-states"></a>处理 IRP \_ MN \_ 查询 \_ 电源的设备电源状态





设备查询-power IRP 会查询单个设备的状态更改，并将其发送到设备堆栈中的所有驱动程序。 此类 IRP 在 i/o 堆栈位置的 DevicePowerState **成员中** 指定了 **DevicePowerState** 。

驱动程序在传递堆栈时处理查询电源 Irp。

如果满足以下任一条件，则函数或筛选器驱动程序可能会导致 [**IRP \_ MN \_ 查询 \_ 电源**](./irp-mn-query-power.md) 请求失败：

-   设备启用了唤醒，并且请求的电源状态低于设备可用于唤醒系统的状态。 例如，可以从 D2 而不是 D3 唤醒系统的设备将无法查询 D3，但会成功查询 D2。

-   进入请求状态将强制驱动程序放弃会丢失数据的操作，如打开的调制解调器连接。 出于此原因，驱动程序很少导致查询失败;在大多数情况下，应用程序会处理这种情况。

若要使 [**IRP \_ MN \_ 查询 \_ 电源**](./irp-mn-query-power.md) 请求失败，驱动程序需要执行以下步骤：

1.  调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) ，以指示驱动程序已准备好处理下一个电源 IRP。 仅 (Windows Server 2003、Windows XP 和 Windows 2000。 ) 

2.  将 **Irp- &gt; IoStatus** 设置为失败状态并调用 [**IOCOMPLETEREQUEST**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)，同时指定 IO \_ NO \_ 增量。 驱动程序不会沿着设备堆栈进一步向下传递 IRP。

3.  从其 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程返回错误状态。

如果驱动程序成功执行了查询-power IRP，则它不能启动任何操作，也不会执行任何其他操作，否则会阻止其成功完成后续 **IRP \_ MN \_ \_** 为查询电源状态的请求。

成功完成 IRP 的驱动程序必须为用于查询状态的集电源 IRP 做好准备，并按如下所示向下传递查询 IRP：

1.  完成所有未完成的 i/o 操作。

2.  为传入 i/o 请求排队。

3.  避免启动会干扰转换到指定电源状态的任何其他新活动。 但是，驱动程序不应保存设备上下文或执行其他步骤来关闭。

4.  调用 **IoCopyCurrentIrpStackLocationToNext** 以设置下一个较低驱动程序的 IRP 堆栈位置。

5.  设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 在 *IoCompletion* 例程中，调用 **PoStartNextPowerIrp** (Windows SERVER 2003、windows XP 和 windows 2000 仅) 指示驱动程序准备就绪，以便处理下一个电源 IRP。

6.  在 windows 7 和 Windows Vista 中调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) () 或 windows Server 2003、windows XP 和 windows 2000) 中的 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (，将 query IRP 传递到下一个较低版本的驱动程序。 不要完成 IRP。

7.  返回状态为 " \_ 挂起"。 驱动程序不得更改 **&gt; IoStatus** 的值。

当查询-power IRP 达到总线驱动程序时，如果驱动程序可以更改为指定电源状态，则总线驱动程序将调用 **PoStartNextPowerIrp** (仅) windows Server 2003、windows XP 和 windows 2000，并将 IoStatus 状态设置为 "成功" **&gt; 。** \_ 然后，总线驱动程序调用 **IoCompleteRequest**，指定 IO \_ 无 \_ 增量。

典型设备堆栈中的驱动程序处理设备查询-power IRP，如下所示：

-   大多数筛选器驱动程序只需将 IRP 传递到下一个较低的驱动程序 (请参阅 [通过电源 irp](passing-power-irps.md)) 并返回状态 " \_ 挂起"。 但是，某些筛选器驱动程序可能首先需要执行特定于设备的任务，例如将传入的 Irp 排队或保存设备电源状态。

-   函数驱动程序执行特定于设备的任务 (例如，完成挂起的 i/o 请求，排队传入 i/o 请求，保存设备上下文，或更改设备电源) ，设置 *IoCompletion* 例程，并将设备电源 irp 传递到下一个较低的驱动程序 (参阅 [通过电源](passing-power-irps.md) irp) 。 它 \_ 从其 *DispatchPower* 例程返回 "挂起" 状态。

-   总线驱动程序调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) (仅) windows Server 2003、windows XP 和 windows 2000 来启动下一个 power IRP。 然后，它将完成 IRP，同时指定 IO \_ 无 \_ 增量。 如果驱动程序无法立即完成 IRP，它将调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，并返回 \_ 其 *DispatchPower* 例程的 "挂起" 状态，并在以后完成 irp。

即使目标设备已处于查询的电源状态，每个函数或筛选器驱动程序也必须将 i/o 排队，并将 IRP 向下传递到下一个较低的驱动程序。 IRP 必须按设备堆栈向下移动到总线驱动程序，这将完成该过程。

处理 **IRP \_ MN \_ 查询 \_ 电源** 请求时，驱动程序应尽快从 *DispatchPower* 例程返回。 对于由处理同一 IRP 的代码发出信号的内核事件，驱动程序不得在其 *DispatchPower* 例程中等待。 由于 power Irp 在整个系统中同步，因此可能会发生死锁。

 

