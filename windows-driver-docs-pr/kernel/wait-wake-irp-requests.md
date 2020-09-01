---
title: 等待/唤醒 IRP 请求
description: 等待/唤醒 IRP 请求
ms.assetid: c67d6dcb-f4a9-4df0-abb8-9d84fc44ec40
keywords:
- 正在发送等待/唤醒 Irp
- 启用了唤醒信号的 WDK 内核
- 等待/唤醒 Irp WDK 电源管理，发送
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45d005852985127a517b9da1e11a660335883466
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187875"
---
# <a name="waitwake-irp-requests"></a>等待/唤醒 IRP 请求





若要发送 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md)，驱动程序将调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)，将 (中的其他参数传递给其他参数) 指向目标 PDO、系统电源状态和指向回调例程的指针。

系统电源状态指定此 IRP 从中唤醒系统的最小可用状态。 该值必须等于或大于[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中的[**SystemWake**](systemwake.md)状态。 例如，如果驱动程序通过 IRP 传递 **PowerSystemSleeping2** ，则关联的 IRP 可能会导致系统从状态 S0、S1 和 S2 中唤醒。 在这种情况下，系统必须支持 S0 和 S2 (范围内的最高和最低的状态) 但不需要支持 S1。

每个请求等待/唤醒 IRP 的驱动程序都应指定一个 [回调例程](wait-wake-callback-routines.md)，该例程将在所有其他驱动程序完成 IRP 后调用。 在这种情况下，驱动程序可以执行任何必要的操作，以将其设备恢复到工作状态。

为响应 **PoRequestPowerIrp**，电源管理器使用次要代码 **IRP \_ MN \_ 等待 \_ 唤醒** 分配一个电源 IRP，并将其发送到目标 PDO 的设备堆栈顶部。 调用方返回指向分配的 IRP 的指针，如果必须取消 IRP，它可以在以后使用。

如果未发生错误，则 **PoRequestPowerIrp** 返回状态 " \_ 挂起"。 此状态表示 IRP 已成功发送并等待完成。

等待/唤醒 IRP 不会更改系统或设备的电源状态。 它只是启用设备的唤醒信号。 IRP 始终处于挂起状态，直到外部信号导致系统或设备唤醒。

 

