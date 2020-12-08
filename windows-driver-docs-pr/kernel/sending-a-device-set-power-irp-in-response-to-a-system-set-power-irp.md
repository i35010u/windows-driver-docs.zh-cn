---
title: 在系统 Set-Power IRP 响应中发送设备 Set-Power IRP
description: 在系统 Set-Power IRP 响应中发送设备 Set-Power IRP
keywords:
- 正在发送设置-电源 Irp
- 设置电源 Irp WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e93684d73b2b645c0e7e69ca28005e42aa24afe5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822279"
---
# <a name="sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp"></a>在系统 Set-Power IRP 响应中发送设备 Set-Power IRP





设备电源策略所有者应执行以下步骤来响应系统设置-电源 IRP：

1.  调用 [**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，将当前 IRP 作为 *Tag* 参数传递，以确保在处理 power IRP 时，驱动程序不会收到即插即用 [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。

    如果 **IoAcquireRemoveLock** 返回失败状态，驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成请求，然后返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应该首先调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，然后调用 **IOCOMPLETEREQUEST** 来完成 IRP，然后返回失败状态。

2.  通过调用 [**IoCopyCurrentIrpStackLocationToNext**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)设置下一个较低驱动程序的 IRP 堆栈位置。

3.  在系统设置-power IRP 中设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。

4.  调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) ，将系统设置-power IRP 标记为挂起。

5.  从 windows Server 2003、Windows XP 和 Windows 2000) 中的 Windows Vista) 或 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (开始 (调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，将系统设置-power IRP 传递到下一个较低版本的驱动程序。

6.  \_从其 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程返回的状态为 "挂起"。

在 *IoCompletion* 例程 (参阅前面列表中的步骤 3) ，设备电源策略所有者将按如下所示发送设备集-电源 IRP：

1.  检查系统设置-power IRP 以获取请求的系统电源状态。 为该系统电源状态选择相应的设备电源状态。 有关详细信息，请参阅 [确定正确的设备电源状态](determining-the-correct-device-power-state.md)。

2.  调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 为在步骤1中确定的设备电源状态发送 [**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) 。 电源策略所有者必须发送设备电源请求，即使设备已处于该状态也是如此。

3.  在对 **PoRequestPowerIrp** 的调用中指定电源完成回调例程 (*CompletionFunction*) ，并在 *上下文* 缓冲区中传递系统设置-power IRP。

4.  返回状态 \_ \_ \_ *IoCompletion* 例程所需的更多处理，以便驱动程序可以完成对系统设置-power IRP 在电源完成回调例程中的处理。

请记住，设备电源策略所有者不仅发送设备集-电源 IRP，还必须在通过设备堆栈传输时处理此 IRP。 因此，设备电源策略所有者可能不仅有与设备设置-电源 irp 关联的电源完成回调例程，还可能具有系统集电源 IRP 的 *IoCompletion* 例程，还可能包含设备设置-电源 Irp 的 *IoCompletion* 例程。 有关详细信息，请参阅 [处理 IRP \_ MN \_ 设置 \_ 设备电源状态的电源](handling-irp-mn-set-power-for-device-power-states.md)。

在 i/o 管理器调用了所有已设置为设备堆栈的 *IoCompletion* 例程后，i/o 管理器将调用该电源完成回调例程。 此时，堆栈中的所有驱动程序都已完成设备设置-电源 IRP，设备电源转换已完成。

电源完成回调例程必须执行以下操作：

1.  调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 以启动下一个 power IRP。 仅 (Windows Server 2003、Windows XP 和 Windows 2000。 ) 

2.  完成系统设置-power IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，并为设备设置-电源 irp 返回状态。

3.  调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 以释放以前获取的锁。

4.  返回设置电源 Irp 完成时所用的状态。

 

