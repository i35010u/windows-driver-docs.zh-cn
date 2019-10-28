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
ms.openlocfilehash: de8f938e955f5f8ef06170009c9ddb71afa36c5a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838516"
---
# <a name="passing-power-irps"></a>传递电源 IRP





电源 Irp 必须按设备堆栈向下传递到 PDO，以确保能够完全管理电源转换。 驱动程序处理 IRP，该 IRP 可在 IRP 向下传播到设备堆栈时降低设备的电源。 驱动程序处理 IRP，该 IRP 在 IRP 在设备堆栈上传输时，应用[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程中的设备功能。

下图显示了在 Windows 7 和 Windows Vista 中，驱动程序需要执行哪些步骤才能将电源 IRP 向下传递到设备堆栈中。

![说明如何通过 windows vista 中的电源 irp](images/passirpvista.png)

如上图所示，在 Windows 7 和 Windows Vista 中，驱动程序必须执行以下操作：

1.  如果设置*IoCompletion*例程，则调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) ; 如果未设置*IoCompletion*例程，则调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 。

    这两个例程设置下一个较低驱动程序的 IRP 堆栈位置。 复制当前堆栈位置可确保在运行*IoCompletion*例程时 IRP 堆栈指针设置为正确的位置。

    如果编写错误的驱动程序会导致错误调用**IoSkipCurrentIrpStackLocation** ，然后设置完成例程，则此驱动程序可能会覆盖由其下的驱动程序设置的完成例程。

2.  如果需要完整的例程，请调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)来设置*IoCompletion*例程。

3.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将 IRP 传递到堆栈中的下一个较低的驱动程序。

下图显示了在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序需要采取哪些步骤才能将电源 IRP 向下传递到设备堆栈中。

![传递电源 irp （windows server 2003、windows xp 和 windows 2000）](images/passirp.png)

如上图所示，驱动程序必须执行以下操作：

1.  根据驱动程序的类型，可能会调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)。 有关详细信息，请参阅[调用 PoStartNextPowerIrp](calling-postartnextpowerirp.md)。

2.  如果设置*IoCompletion*例程，则调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext) ; 如果未设置*IoCompletion*例程，则调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 。

    这两个例程设置下一个较低驱动程序的 IRP 堆栈位置。 复制当前堆栈位置可确保在运行*IoCompletion*例程时 IRP 堆栈指针设置为正确的位置。

3.  调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)以设置*IoCompletion*例程。 在*IoCompletion*例程中，大多数驱动程序都[调用 PoStartNextPowerIrp](calling-postartnextpowerirp.md) ，以指示它已准备好处理下一个电源 IRP。

4.  调用[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)将 IRP 传递到堆栈中的下一个较低的驱动程序。

    驱动程序必须使用**PoCallDriver**，而不是**IoCallDriver** （与其他 irp 相同），以确保系统正确同步 power irp。 有关详细信息，请参阅[调用 IoCallDriver 与调用 PoCallDriver](calling-iocalldriver-versus-calling-pocalldriver.md)。

请记住， *IoCompletion*例程可以在 IRQL = 调度\_级别调用。 因此，如果在较低级别的驱动程序已使用 IRP 完成后，驱动程序需要在 IRQL = 被动\_级别进行额外处理，则驱动程序的完成例程应将工作项排队，然后返回状态\_更多\_处理 @no__需要 t_3_。 工作线程必须完成 IRP。

在 Windows 98/Me 中，驱动程序必须以 IRQL = 被动\_级别完成电源 Irp。

### <a name="do-not-change-the-function-codes-in-a-power-irp"></a>不要更改 Power IRP 中的函数代码

除了控制 Irp 处理的常用规则， [**IRP\_MJ\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)irp 具有以下特殊要求：接收 POWER irp 的驱动程序不得更改中任何 i/o 堆栈位置的主要和次要函数代码由 power manager 或更高级别的驱动程序设置的 IRP。 在完成 IRP 之前，power manager 依赖于这些函数代码保持不变。 违反此规则会导致难以调试的问题。 例如，操作系统可能会停止响应或 "挂起"。

### <a name="do-not-block-while-handling-a-power-irp"></a>处理 Power IRP 时不阻止

驱动程序在处理电源 Irp 时不得产生长时间的延迟。

当传递电源 IRP 时，驱动程序应在调用**IoCallDriver** （在 windows 7 和 windows Vista 中）或**PoCallDriver** （在 Windows SERVER 2003、windows XP 和 windows 2000 中）后，尽快从其[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回. 在返回之前，驱动程序不得等待内核事件或延迟。 如果驱动程序无法在短暂的时间内处理 power IRP，它应返回状态\_"挂起"，并将所有传入的 Irp 排队，直到电源 IRP 完成。 （请注意，此行为不同于允许阻止的 PnP Irp 和[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程的行为。）

如果驱动程序必须在设备堆栈后面的其他驱动程序等待电源操作，它应返回状态\_" *DispatchPower* " 例程挂起，并为电源 IRP 设置*IoCompletion*例程。 驱动程序可以在*IoCompletion*例程中执行所需的任何任务，然后调用**PoStartNextPowerIrp** （仅限 Windows SERVER 2003、windows XP 和 Windows 2000）和[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)。

例如，设备的电源策略所有者通常会在保留系统电源 IRP 的同时发送设备电源 IRP，以便设置适合于所请求系统电源状态的设备电源状态。

在这种情况下，电源策略所有者应在系统电源 IRP 中设置一个*IoCompletion*例程，将系统电源 irp 传递到下一个较低的驱动程序，并从其*DISPATCHPOWER*例程返回状态\_"。

在*IoCompletion*例程中，它调用**PoRequestPowerIrp**来发送设备电源 IRP，并将指针传递到请求中的回调例程。 *IoCompletion*例程应返回状态\_\_需要更多的\_处理。

最后，驱动程序从回调例程向下传递系统 IRP。 驱动程序不得在其*DispatchPower*例程中等待内核事件，并使用*IoCompletion*例程为当前正在处理的 IRP 发出信号;可能会发生系统死锁。 有关详细信息，请参阅[在设备电源策略所有者中处理系统集电源 IRP](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。

在类似情况下，当系统进入睡眠状态时，电源策略所有者可能需要先完成一些挂起的 i/o，然后才能将设备 IRP 关闭并关闭其设备。 驱动程序应将工作项排队，并返回状态\_在*DispatchPower*例程中挂起，而不是在 i/o 完成并在其*DispatchPower*例程中等待时发出事件。 在工作线程中，它等待 i/o 完成，然后发送设备电源 IRP。 有关详细信息，请参阅[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)。

 

 




