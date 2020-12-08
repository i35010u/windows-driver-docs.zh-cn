---
title: 处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP
description: 处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP
keywords:
- 正在接收等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，接收
- 函数驱动程序 WDK 电源管理
- FDOs WDK 电源管理
- 筛选器 DO WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f641627d55d284eb6eb50d5f1f76c510fe1dd11c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820663"
---
# <a name="handling-a-waitwake-irp-in-a-function-fdo-or-filter-driver-filter-do"></a>处理函数 (FDO) 或筛选器驱动程序（筛选器 DO）中的等待/唤醒 IRP





当创建 FDO 或筛选器的驱动程序确实收到关联 PDO 的 [**IRP \_ MN \_ WAIT \_ 唤醒**](./irp-mn-wait-wake.md) 请求时，它可以直接将 irp 传递到下一个较低的驱动程序，或在传递 IRP 之前执行某些操作。

### <a name="for-devices-that-support-wake-up"></a>对于支持 Wake-Up 的设备

接收到等待/唤醒 IRP 后，函数或筛选器驱动程序应执行以下步骤：

1.  调用 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保在处理 wait/唤醒 IRP 时，驱动程序不会接收 PnP [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。

    如果 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) 返回失败状态，驱动程序不应继续处理 IRP。 相反，它会完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，并返回失败状态。

2.  检查 **&gt; WaitWake PowerState** 的值，并将当前设备电源状态与 **DeviceState** \[ \] [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中的 DeviceState SystemWake 进行比较。

    如果设备支持唤醒，但不支持从指定的 [SystemWake](systemwake.md) 状态进行唤醒，或者不是从当前设备电源状态进行的，则该驱动程序应使 IRP 失败，如下所示：

    -   设置状态 \_ 无效的 \_ 设备 \_ 状态 **- &gt; IoStatus。状态**。
    -   完成 IRP (**IoCompleteRequest**) ，同时指定 IO 无增量的优先级 \_ 提升 \_ 。
    -   返回 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程的 **&gt; IoStatus** 中设置的状态。

3.  否则，请使用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)为 IRP 设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 *IoCompletion* 例程应执行驱动程序将设备返回到工作状态所需的任何任务。

    如果已取消 IRP，还将调用 *IoCompletion* 例程。

4.  保存驱动程序在其 *IoCompletion* 例程中可能需要的所有信息。

5.  在 windows 7 和 Windows Vista 中调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) () 或 windows Server 003、windows XP 和 windows 2000) 中的 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (，以将等待/唤醒 IRP 传递到下一个较低版本的驱动程序。

6.  调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 以释放以前获取的锁。

7.  \_从 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回的状态为 "挂起"。 驱动程序在保存 IRP 时不得更改 **&gt; IoStatus** 中的值。

### <a name="for-devices-that-do-not-support-wake-up"></a>对于不支持 Wake-Up 的设备

如果函数或筛选器驱动程序接收到不支持唤醒功能的设备的等待/唤醒 IRP，则该驱动程序应该会使 IRP 失败，如下所示：

1.  完成 IRP (**IoCompleteRequest**) ，同时指定 IO 无增量的优先级 \_ 提升 \_ 。

2.  返回 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程的 **&gt; IoStatus** 中设置的状态。

 

