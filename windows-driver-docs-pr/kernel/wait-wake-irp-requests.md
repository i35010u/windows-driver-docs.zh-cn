---
title: 等待/唤醒 IRP 请求
description: 等待/唤醒 IRP 请求
ms.assetid: c67d6dcb-f4a9-4df0-abb8-9d84fc44ec40
keywords:
- 发送等待/唤醒 Irp
- 唤醒信号启用 WDK 内核
- 等待/唤醒 Irp WDK 电源管理发送
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c08b0f0a7a51accbccadec3e05ba797777acf418
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358134"
---
# <a name="waitwake-irp-requests"></a>等待/唤醒 IRP 请求





若要发送[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)，驱动程序调用[ **PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)，指向目标 PDO、 系统电源状态和指向回调例程的指针，则传递 （以及其他参数）。

系统电源状态指定此 IRP 可以将系统唤醒从其提供最低支持的状态。 值必须等于或比更供电[ **SystemWake** ](systemwake.md)状态处于[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构。 例如，如果驱动程序将传递**PowerSystemSleeping2** IRP，在关联的 IRP 可能会导致系统以从 S0、 S1 和 S2 的状态中唤醒。 在这种情况下，系统必须支持 S0 和 S2 （最高和最低的功率状态范围中） 但需要支持 S1。

请求等待/唤醒 IRP 每个驱动程序应指定[回调例程](wait-wake-callback-routines.md)，所有其他驱动程序完成 IRP 后调用。 在此例程，该驱动程序可以执行会尽一切努力将其设备恢复至工作状态。

以响应**PoRequestPowerIrp**，电源管理器分配具有细微的代码的能力 IRP **IRP\_MN\_等待\_唤醒**并将其发送到设备的顶部目标 PDO 堆栈。 调用方返回一个指针，到已分配的 IRP，它可以使用更高版本是否必须取消 IRP。

如果不发生任何错误， **PoRequestPowerIrp**将返回状态\_PENDING。 此状态表示 IRP 已成功发送，并且正在等待完成。

等待/唤醒 IRP 不会更改的系统或设备的电源状态。 它只是让设备的唤醒信号。 IRP 保持挂起之前对外部信号会导致系统或设备被唤醒。

 

 




