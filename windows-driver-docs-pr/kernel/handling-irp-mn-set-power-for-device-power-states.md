---
title: 处理设备电源状态的 IRP_MN_SET_POWER
description: 处理设备电源状态的 IRP_MN_SET_POWER
keywords:
- IRP_MN_SET_POWER
- 设备电源状态 WDK 内核
- 设置-power Irp WDK 内核
- DispatchPower 例程
- 将 Irp 向下传递设备堆栈 WDK
- 设备设置电源 Irp WDK 内核
- power Irp WDK 内核，设备更改
- 调度例程 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dded567a565e20d442b296ef3e4e1e94d1ccdd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821437"
---
# <a name="handling-irp_mn_set_power-for-device-power-states"></a>处理 IRP \_ MN \_ 设置 \_ 设备电源状态的电源





设备设置-power IRP 请求为单个设备更改状态，并将其发送到设备堆栈中的所有驱动程序。 此类 IRP 在 i/o 堆栈位置的 DevicePowerState **成员中** 指定了 **DevicePowerState** 。

驱动程序在关闭后，会处理关闭的 Irp。 对于开机 Irp，驱动程序将 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程设置为 irp 向下传递堆栈，然后处理 *IoCompletion* 例程中的 irp，因为 irp 将在堆栈上传输。 典型设备堆栈中的驱动程序将处理设备集电源 IRP，如下所示：

-   大多数筛选器驱动程序只需调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，然后将 IRP 传递到下一个较低的驱动程序 (请参阅 [通过电源 Irp](passing-power-irps.md)) ，并 \_ 从 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程返回挂起状态。 但是，某些筛选器驱动程序可能首先需要执行特定于设备的任务，例如将传入的 Irp 排队或保存设备电源状态。

-   函数驱动程序调用 **也**，执行特定于设备的任务 (例如，完成挂起的 i/o 请求、对传入 i/o 请求排队、保存设备上下文或更改设备电源) 、设置 *IoCompletion* 例程（如有必要），并将设备电源 irp 传递到下一个较低的驱动程序 (请参阅 [通过 power irp](passing-power-irps.md)) 。 它 \_ 从其 *DispatchPower* 例程返回 "挂起" 状态。

-   如果总线驱动程序能够执行此操作，则该驱动程序将更改设备电源，并调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 通知电源管理器新设备电源状态。 仅在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序还必须调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) ，以在设置电源状态后启动下一个 power IRP。 然后，该驱动程序完成 IRP，指定 IO \_ 无 \_ 增量。 如果驱动程序无法立即完成 IRP，它将调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，并返回 \_ 其 *DispatchPower* 例程的 "挂起" 状态，并在以后完成 irp。

即使目标设备已处于 "已请求" 电源状态，每个函数或筛选器驱动程序也必须将 IRP 向下传递到下一个较低版本的驱动程序。 每个设置电源 IRP 都必须按设备堆栈向下移动到总线驱动程序，这将完成该过程。

位于总线驱动程序之上的函数和筛选器驱动程序不能使设备集的电源 IRP 失败。 如果设备被删除或正在被删除，则总线驱动程序可以使设备开启 IRP 失败。

驱动程序堆栈中 (函数、筛选器和总线驱动程序) 的每个驱动程序都必须调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) ，以通知 power manager 其相应设备对象的电源状态发生变化。

与与设备电源和电源线相关联的其他驱动程序任务一样，如果新状态为 D0) 或在设备关闭 (之前， **PoSetPowerState** 的调用必须在设备接通电源 (后发生，如果新状态是) 的任何其他状态。

每个驱动程序都应跟踪其设备的电源状态。 电源管理器不会将此信息提供给驱动程序。

处理 [**IRP \_ MN \_ 设置 \_**](./irp-mn-set-power.md) 设备电源状态的电源请求时，驱动程序应该尽快从 *DispatchPower* 例程返回。 对于由处理同一 IRP 的代码发出信号的内核事件，驱动程序不得在其 *DispatchPower* 例程中等待。 由于 power Irp 在整个系统中同步，因此可能会发生死锁。

为确保最高级别的系统性能（特别是对于多媒体应用程序），驱动程序应在中断请求级别执行耗时的操作， (IRQL) 等于被动 \_ 级别。 若要执行 IRQL = 被动级别的操作 \_ ，驱动程序可以使用 [专用线程](device-dedicated-threads.md) 或 [系统工作线程](system-worker-threads.md)。 有关优化多媒体平台驱动程序性能的指南，请参阅 [流媒体设备设计指南](../stream/index.md)。

驱动程序处理 power IRP 所需的确切步骤取决于设备是否通电或断电，如以下部分中所述：

[处理设备断电 IRP](handling-device-power-down-irps.md)

[处理设备通电 IRP](handling-device-power-up-irps.md)

 

