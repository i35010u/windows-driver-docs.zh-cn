---
title: 等待/唤醒回调例程
description: 等待/唤醒回调例程
ms.assetid: 55749f14-37eb-45d9-8a2c-9ebf7fb3bc75
keywords:
- 正在发送等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理，发送
- 回调例程 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c30347bf10b25e9a19a06d225e018dce2db47946
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838323"
---
# <a name="waitwake-callback-routines"></a>等待/唤醒回调例程





当驱动程序请求 wait/唤醒 IRP 时，它必须指定回调例程，以便在唤醒事件发生时将设备返回到工作状态（D0）。 发生唤醒事件并且所有驱动程序都已完成 IRP 后，系统会调用传递给[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)的回调例程。

由于此回调例程是代表生成 IRP 的驱动程序（而不是处理 IRP 的驱动程序）设置的，因此不能调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp);只有设置为驱动程序的[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程才会将 IRP 向下传递到堆栈，并应启动下一个 power IRP。 请记住，策略所有者不仅发送 IRP，还会处理它，因此，它可能会设置*IoCompletion*例程，因为它会将 irp 向下传递到堆栈，同时还会在请求等待/唤醒 IRP 时设置回调例程。

回调例程具有以下职责：

1.  如果驱动程序控制多个设备，确定其设备发出唤醒信号。

2.  服务导致唤醒信号的事件。

3.  通过调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)发送**PowerDeviceD0**请求，将设备设置为处于 D0 状态的唤醒状态。 驱动程序还必须调用[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) ，以通知电源管理器新设备电源状态。 有关详细信息，请参阅[发送 IRP\_MN\_QUERY\_POWER OR IRP\_MN\_为设备电源状态设置\_功率](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)。

4.  如果驱动程序为 IRP 设置了[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程，请调用[**IoSetCancelRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)将*Cancel*例程重置为**NULL**。

5.  如果驱动程序拥有多个设备的电源策略，则减小其等待/唤醒引用计数。 如果计数不为零，表示其他设备以前发送了等待/唤醒 IRP，请为其 PDO 请求其他等待/唤醒 IRP （**PoRequestPowerIrp**）。

    例如，PCI 设备可能对调制解调器和网络接口卡（NIC）启用了 "等待/唤醒"。 如果 NIC 唤醒系统（进而完成 IRP），PCI FDO 必须将另一个等待/唤醒 IRP 发送到其自身，以便调制解调器仍可以唤醒。

由于请求 wait/唤醒 IRP 的驱动程序控制其设备堆栈的电源策略，因此它负责在 IRP 完成后将其设备返回到工作状态。 尽管较小的驱动程序可能已物理应用到设备，但策略所有者必须调用**PoRequestPowerIrp**来发送**IRP\_MN\_集\_power** Request 设备电源状态 D0。 只有在设备堆栈中的所有驱动程序都已处理后，设备才会恢复到工作状态。

 

 




