---
title: 在系统 Set-Power IRP 响应中发送设备 Set-Power IRP
description: 在系统 Set-Power IRP 响应中发送设备 Set-Power IRP
ms.assetid: b2029292-d770-4095-8bd7-9358b282216c
keywords:
- 正在发送设置-电源 Irp
- 设置电源 Irp WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d149b7fcf21c3f242a13dd990ca11b0aaf25109f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836373"
---
# <a name="sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp"></a>在系统 Set-Power IRP 响应中发送设备 Set-Power IRP





设备电源策略所有者应执行以下步骤来响应系统设置-电源 IRP：

1.  调用[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)，将当前 IRP 作为*Tag*参数传递，以确保驱动程序未收到即插即用[**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)在处理 power IRP 时删除\_设备请求。

    如果**IoAcquireRemoveLock**返回失败状态，驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成请求，然后返回失败状态。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序应该首先调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，然后调用**IOCOMPLETEREQUEST**来完成 IRP，然后返回失败状态。

2.  通过调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)设置下一个较低驱动程序的 IRP 堆栈位置。

3.  在系统设置-power IRP 中设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。

4.  调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，将系统设置-power IRP 标记为挂起。

5.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （从 windows Vista 开始）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （在 Windows SERVER 2003、windows XP 和 windows 2000 中），将系统设置-power IRP 传递到下一个较低版本的驱动程序。

6.  返回状态从其[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程挂起\_。

在*IoCompletion*例程中（请参阅前面的列表中的步骤3），设备电源策略所有者会按如下所示发送设备集-电源 IRP：

1.  检查系统设置-power IRP 以获取请求的系统电源状态。 为该系统电源状态选择相应的设备电源状态。 有关详细信息，请参阅[确定正确的设备电源状态](determining-the-correct-device-power-state.md)。

2.  调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)发送[**IRP\_MN\_设置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)在步骤1中确定的设备电源状态的\_电源。 电源策略所有者必须发送设备电源请求，即使设备已处于该状态也是如此。

3.  在对**PoRequestPowerIrp**的调用中指定一个电源完成回调例程（*CompletionFunction*），并在*上下文*缓冲区中传递系统设置-power IRP。

4.  返回状态\_需要从*IoCompletion*例程处理更多\_处理\_，以便驱动程序可以完成完成电源完成回调例程中的系统集电源 IRP 处理。

请记住，设备电源策略所有者不仅发送设备集-电源 IRP，还必须在通过设备堆栈传输时处理此 IRP。 因此，设备电源策略所有者可能不仅有与设备设置-电源 IRP 关联的电源完成回调例程，还可能具有系统集电源 IRP 的*IoCompletion* *例程，还可能是*设备设置-电源 IRP。 有关详细信息，请参阅[处理 IRP\_MN\_设置设备电源状态\_电源](handling-irp-mn-set-power-for-device-power-states.md)。

在 i/o 管理器调用了所有已设置为设备堆栈的*IoCompletion*例程后，i/o 管理器将调用该电源完成回调例程。 此时，堆栈中的所有驱动程序都已完成设备设置-电源 IRP，设备电源转换已完成。

电源完成回调例程必须执行以下操作：

1.  调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)以启动下一个 power IRP。 （仅限 windows Server 2003、Windows XP 和 Windows 2000。）

2.  完成系统设置-power IRP （[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)），并为设备设置-电源 irp 返回状态。

3.  调用[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)以释放以前获取的锁。

4.  返回设置电源 Irp 完成时所用的状态。

 

 




