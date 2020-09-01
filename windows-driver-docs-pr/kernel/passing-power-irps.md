---
title: 传递电源 IRP
description: 传递电源 IRP
ms.assetid: 01473eb0-ae60-4a95-9ae7-97b2b982d3d1
keywords:
- power Irp WDK 内核，通过
- 将 Irp 向下传递设备堆栈 WDK
- DispatchPower 例程
- 调度例程 WDK 电源管理
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fdcf0d166184fc956db2aa46e58b6024e3a9f30
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187061"
---
# <a name="passing-power-irps"></a>传递电源 IRP





电源 Irp 必须按设备堆栈向下传递到 PDO，以确保能够完全管理电源转换。 驱动程序处理 IRP，该 IRP 可在 IRP 向下传播到设备堆栈时降低设备的电源。 驱动程序处理 IRP，该 IRP 在 IRP 在设备堆栈上传输时，应用 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程中的设备功能。

下图显示了在 Windows 7 和 Windows Vista 中，驱动程序需要执行哪些步骤才能将电源 IRP 向下传递到设备堆栈中。

![说明如何通过 windows vista 中的电源 irp](images/passirpvista.png)

如上图所示，在 Windows 7 和 Windows Vista 中，驱动程序必须执行以下操作：

1.  如果设置*IoCompletion*例程，则调用[**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) ; 如果未设置*IoCompletion*例程，则调用[**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 。

    这两个例程设置下一个较低驱动程序的 IRP 堆栈位置。 复制当前堆栈位置可确保在运行 *IoCompletion* 例程时 IRP 堆栈指针设置为正确的位置。

    如果错误编写的驱动程序在调用 **IoSkipCurrentIrpStackLocation** 时出错，然后设置完成例程，则此驱动程序可能会覆盖其下级驱动程序设置的完成例程。

2.  如果需要完整的例程，请调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 来设置 *IoCompletion* 例程。

3.  调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将 IRP 传递到堆栈中的下一个较低的驱动程序。

下图显示了在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序需要采取哪些步骤才能将电源 IRP 向下传递到设备堆栈中。

![将电源 irp 传递 (windows server 2003、windows xp 和 windows 2000) ](images/passirp.png)

如上图所示，驱动程序必须执行以下操作：

1.  根据驱动程序的类型，可能会调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)。 有关详细信息，请参阅 [调用 PoStartNextPowerIrp](calling-postartnextpowerirp.md)。

2.  如果设置*IoCompletion*例程，则调用[**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) ; 如果未设置*IoCompletion*例程，则调用[**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 。

    这两个例程设置下一个较低驱动程序的 IRP 堆栈位置。 复制当前堆栈位置可确保在运行 *IoCompletion* 例程时 IRP 堆栈指针设置为正确的位置。

3.  调用 [**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 以设置 *IoCompletion* 例程。 在 *IoCompletion* 例程中，大多数驱动程序都 [调用 PoStartNextPowerIrp](calling-postartnextpowerirp.md) ，以指示它已准备好处理下一个电源 IRP。

4.  调用 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) 将 IRP 传递到堆栈中的下一个较低的驱动程序。

    对于其他 Irp) ，驱动程序必须使用 **PoCallDriver**而不是 **IoCallDriver** (，以确保系统正确同步 power irp。 有关详细信息，请参阅 [调用 IoCallDriver 与调用 PoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)。

请记住， *IoCompletion* 例程可以在 IRQL = 调度 \_ 级别调用。 因此，如果在 \_ 较低级别的驱动程序已使用 IRP 完成后，驱动程序需要在 IRQL = 被动级别进行额外处理，则驱动程序的完成例程应将工作项排队，然后返回 \_ \_ 所需的状态更多处理 \_ 。 工作线程必须完成 IRP。

在 Windows 98/Me 中，驱动程序必须以 IRQL = 被动级别完成电源 Irp \_ 。

### <a name="do-not-change-the-function-codes-in-a-power-irp"></a>不要更改 Power IRP 中的函数代码

除了控制对 Irp 的处理的常规规则外， [**IRP \_ MJ \_ 电源**](./irp-mj-power.md) irp 还具有以下特殊要求：接收 power IRP 的驱动程序不得更改 IRP 中任何 i/o 堆栈位置的主要和次要函数代码，这些位置已由 POWER manager 或高级驱动程序设置。 在完成 IRP 之前，power manager 依赖于这些函数代码保持不变。 违反此规则会导致难以调试的问题。 例如，操作系统可能会停止响应或 "挂起"。

### <a name="do-not-block-while-handling-a-power-irp"></a>处理 Power IRP 时不阻止

驱动程序在处理电源 Irp 时不得产生长时间的延迟。

当传递电源 IRP 时，驱动程序应在) windows Server 2003、windows XP 和 Windows 2000) 中的 Windows 7 和 Windows Vista 或**PoCallDriver** (中 (调用**IoCallDriver**后尽快从其[*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回。 在返回之前，驱动程序不得等待内核事件或延迟。 如果驱动程序无法在短暂的时间内处理 power IRP，它应返回状态 " \_ 挂起" 并将所有传入的 irp 排队，直到电源 IRP 完成。  (请注意，此行为不同于允许阻止的 PnP Irp 和 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程的行为。 ) 

如果驱动程序必须在设备堆栈后面的其他驱动程序等待电源操作，它应 \_ 从其 *DispatchPower* 例程返回 "挂起" 状态，并为电源 IRP 设置 *IoCompletion* 例程。 驱动程序可以在 *IoCompletion* 例程中执行所需的任何任务，然后调用 **PoStartNextPowerIrp** (仅限 Windows SERVER 2003、windows XP 和 Windows 2000) 和 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

例如，设备的电源策略所有者通常会在保留系统电源 IRP 的同时发送设备电源 IRP，以便设置适合于所请求系统电源状态的设备电源状态。

在这种情况下，电源策略所有者应在系统电源 IRP 中设置一个 *IoCompletion* 例程，将系统电源 irp 传递到下一个较低的驱动程序，并 \_ 从其 *DispatchPower* 例程返回 "挂起" 状态。

在 *IoCompletion* 例程中，它调用 **PoRequestPowerIrp** 来发送设备电源 IRP，并将指针传递到请求中的回调例程。 *IoCompletion*例程应返回 \_ 更多 \_ \_ 所需的状态。

最后，驱动程序从回调例程向下传递系统 IRP。 驱动程序不得在其 *DispatchPower* 例程中等待内核事件，并使用 *IoCompletion* 例程为当前正在处理的 IRP 发出信号;可能会发生系统死锁。 有关详细信息，请参阅 [在设备电源策略所有者中处理系统集电源 IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。

在类似情况下，当系统进入睡眠状态时，电源策略所有者可能需要先完成一些挂起的 i/o，然后才能将设备 IRP 关闭并关闭其设备。 驱动程序应将工作项排队，并在*DispatchPower* \_ *DispatchPower*例程中返回挂起状态，而不是在 I/o 完成并在其 DispatchPower 例程中等待时发出事件。 在工作线程中，它等待 i/o 完成，然后发送设备电源 IRP。 有关详细信息，请参阅 [**IoAllocateWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)。

 

