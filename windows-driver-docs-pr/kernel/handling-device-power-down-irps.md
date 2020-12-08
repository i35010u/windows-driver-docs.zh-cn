---
title: 处理设备断电 IRP
description: 处理设备断电 IRP
keywords:
- 设置-power Irp WDK 内核
- 设备设置电源 Irp WDK 内核
- power Irp WDK 内核，设备更改
- 关闭 Irp WDK 内核
- 上下文信息 WDK 电源管理
- 关闭电源管理 WDK 内核
- 关闭 power WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d47bf6623d65f1f20a5ecd6a2fcd5ff0e027ec15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838463"
---
# <a name="handling-device-power-down-irps"></a>处理设备断电 IRP





设备电源关闭 IRP 指定次要函数代码 [**irp \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 和设备电源状态 (**PowerDeviceD0**、 **PowerDeviceD1**、 **PowerDeviceD2** 或 **PowerDeviceD3**) ，该功能已降低或等于当前设备电源状态。 当 IRP 向下移动设备堆栈时，驱动程序必须处理电源 IRP。 高层驱动程序必须在较低级别的驱动程序之前处理 IRP。 没有要执行的设备特定任务的驱动程序应立即将 IRP 传递到下一个较低版本的驱动程序。

下图显示了处理此类 IRP 所涉及的步骤。

![说明如何处理设备关机请求的关系图](images/devd3.png)

如果 IRP 指定 **PowerDeviceD3**，则函数驱动程序通常应执行以下任务：

-   调用 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，传递当前 IRP，以确保在处理 power irp 时，驱动程序不会收到 PnP [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。

    如果 **IoAcquireRemoveLock** 返回失败状态，驱动程序不应继续处理 IRP。 从 Windows Vista 开始，驱动程序应调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 IRP，然后返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应调用 **IoCompleteRequest** 来完成 IRP，然后调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 来启动下一个 power IRP，然后返回失败状态。

-   执行在删除设备电源之前必须完成的任何特定于设备的任务，例如关闭设备、完成或刷新任何挂起的 i/o、禁用中断、将 [后续传入的 irp 排队](queuing-i-o-requests-while-a-device-is-sleeping.md)以及保存恢复或重新初始化设备的设备上下文。

    驱动程序不应导致长时间的延迟 (例如，在处理 IRP 时，用户可能会发现此类设备) 不合理的延迟。

    驱动程序应将任何传入的 i/o 请求排队，直到设备返回到工作状态。

-   可能检查 **ShutdownType** 中的值。 如果系统设置-power IRP 处于活动状态，则 **ShutdownType** 会提供有关系统 IRP 的信息。 有关此值的详细信息，请参阅 [系统电源操作](system-power-actions.md)。

    休眠路径上设备的驱动程序必须检查此值。 如果 **ShutdownType** 是 **PowerActionHibernate**，则驱动程序应保存恢复设备所需的任何上下文，但不应关闭设备电源。

-   如果驱动程序能够执行此操作，请更改设备的物理电源状态，如果更改适当，则更改。

-   调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 以通知电源管理器新设备电源状态。

-   调用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) 设置下一个较低驱动程序的堆栈位置。

-   设置调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)的 *IoCompletion* 例程，该例程指示驱动程序已准备好处理下一个电源 IRP。 在 Windows 7 和 Windows Vista 中，此步骤不是必需的。

-   在 Windows 7 和 Windows Vista 中调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) () 或在 windows Server 2003、windows XP 和 windows 2000) 中调用 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (，以将 IRP 传递到下一个较低版本的驱动程序。 IRP 必须一直向下传递到完成 IRP 的总线驱动程序。

-   调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 以释放以前获取的锁。

-   返回状态为 " \_ 挂起"。

驱动程序必须保存任何设备上下文信息并在转发 IRP 之前设置新的电源状态。 上下文信息至少应包含请求的新电源状态。 它还应包含驱动程序在开机时需要的任何其他信息。 完成 IRP 并关闭设备后，驱动程序将无法再访问设备，并且设备上下文不可用。

每个驱动程序都必须将 IRP 传递到下一个较低版本的驱动程序。 当 IRP 达到总线驱动程序时，总线驱动程序会关闭设备 (如果它能够) ，将调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 来通知电源管理器并完成 IRP。

但是，如果总线驱动程序为休眠设备服务，则它应检查 IRP 中 **ShutdownType** 的值是否为 PowerSystemHibernate。 如果是这样，则总线驱动程序应调用 **PoSetPowerState** 来报告 PowerDeviceD3，但不应关闭设备电源。 在保存休眠文件以及系统的其余部分后，设备将关闭电源。

在所有子设备关闭后，总线驱动程序也可以选择关闭总线的总线。 此类行为取决于设备。

如果 IRP 指定任何其他状态 (D0、D1 或 D2) ，则必需的驱动程序操作与设备相关。 通常，当 i/o 请求到达时，支持这些状态的设备可快速返回到工作状态。 此类设备的驱动程序必须完成任何挂起的 i/o 请求，将任何新请求排队，并在将 IRP 转发到下一个较低版本的驱动程序之前保存所有必要的上下文。 当 IRP 达到总线驱动程序时，它会将硬件设置为请求状态。 驱动程序无法在设备处于睡眠状态时对其进行访问。

在某些情况下，如果设备已处于 D0 状态，则函数或筛选器驱动程序可能会接收到指定 PowerDeviceD0 的设备电源 IRP。 驱动程序应处理此 IRP，因为它将是任何其他设置-电源 IRP：完成挂起的 i/o 请求，排队传入 i/o 请求，设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，然后将 IRP 向下传递到下一个较低的驱动程序。 但是，驱动程序不能更改设备的硬件设置。 当总线驱动程序收到 IRP 后，只需完成 IRP 即可。 IRP 完成后，函数和筛选器驱动程序可以处理任何排队的请求。 直到 IRP 完成之后，才会将 i/o 排队，从而消除了驱动程序在更高程度上尝试 i/o 时尝试更改设备寄存器的任何可能性。

 

