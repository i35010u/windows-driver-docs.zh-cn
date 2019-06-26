---
title: 等待/唤醒回调例程
description: 等待/唤醒回调例程
ms.assetid: 55749f14-37eb-45d9-8a2c-9ebf7fb3bc75
keywords:
- 发送等待/唤醒 Irp
- 等待/唤醒 Irp WDK 电源管理发送
- 回调例程 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338baece96095bfe3b8efa2457331fdbf1b38582
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358128"
---
# <a name="waitwake-callback-routines"></a>等待/唤醒回调例程





当驱动程序请求等待/唤醒 IRP 时，它必须以便它可以返回至工作状态 (D0) 设备，在发生唤醒事件时指定的回调例程。 发生唤醒事件和所有驱动程序已完成 IRP 后，系统会调用传递给回调例程[ **PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)。

因为此回调例程设置代表发出 IRP 的驱动程序，而不处理 IRP 的驱动程序 — 它不能调用[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp); 仅[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)设置为驱动程序通过在堆栈的下层 IRP 的例程应启动下一步电源 IRP。 请记住，并且策略所有者发送 IRP 不仅能够处理它，因此可能会设置*IoCompletion*传递除了请求等待/唤醒 IRP 时设置的回调例程在堆栈的下层 IRP 例程。

回调例程具有下列职责：

1.  如果该驱动程序控制多台设备，确定哪些其设备发出信号唤醒。

2.  服务导致唤醒信号的事件。

3.  将通过调用来发出信号 D0 状态中唤醒设备设置[ **PoRequestPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)发送**PowerDeviceD0**请求。 该驱动程序还必须调用[ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)通知电源管理器的新设备电源状态。 有关详细信息，请参阅[发送 IRP\_MN\_查询\_电源或 IRP\_MN\_设置\_的电源可用于设备的电源状态](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)。

4.  如果该驱动程序设置[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel) IRP，调用的例程[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)重置*取消*到日常**NULL**。

5.  如果该驱动程序拥有多个设备的电源策略，则递减其等待/唤醒引用计数。 如果计数为非零值，指示的另一台设备以前发送等待/唤醒 IRP，请求另一个等待/唤醒 IRP (**PoRequestPowerIrp**) 对其 PDO。

    例如，PCI 设备可能必须等待/唤醒启用调制解调器和网络接口卡 (NIC)。 如果 NIC 唤醒 （这样就完成了 IRP） 系统，PCI FDO 必须向自身发送另一个等待/唤醒 IRP，以便调制解调器将仍然能够唤醒。

请求等待/唤醒 IRP 控件的驱动程序电源策略及其设备堆栈，因为它负责 IRP 完成时将其设备回到工作状态。 虽然低级驱动程序可能已物理上应用电源到设备，必须调用策略所有者**PoRequestPowerIrp**发送**IRP\_MN\_设置\_POWER**设备电源状态 D0 的请求。 仅在设备堆栈中的所有驱动程序有处理此强化 IRP 后将设备返回到工作状态。

 

 




