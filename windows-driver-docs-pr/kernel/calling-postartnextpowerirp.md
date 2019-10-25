---
title: 调用 PoStartNextPowerIrp
description: 调用 PoStartNextPowerIrp
ms.assetid: 8b3fb578-2ac2-4a04-ac99-1cfd51b07b01
keywords:
- power Irp WDK 内核，PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01721a79c79fcb7f2d25a631722e2a5e0201b8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828579"
---
# <a name="calling-postartnextpowerirp"></a>调用 PoStartNextPowerIrp





从 Windows Vista 开始，调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序在处理查询-power IRP 或集电源 IRP 之后，必须调用**PoStartNextPowerIrp**来通知电源管理器它已准备好接收另一个 power IRP。 当 IRP 堆栈位置指向当前驱动程序并在调用[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)之前，驱动程序必须调用**PoStartNextPowerIrp** 。

驱动程序必须为每个[**IRP\_MN\_QUERY**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)为每个 irp 调用此例程一次，\_Power or [**IRP\_MN\_设置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)它收到\_的 POWER request。 处理 IRP\_MN 时，驱动程序不需要调用**PoStartNextPowerIrp** [ **\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)或[**IRP\_MN\_POWER\_序列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)请求。

当驱动程序调用**PoStartNextPowerIrp**时，当前 IRP 堆栈位置必须指向当前驱动程序。 作为一般规则，此调用最好是从[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程进行。 在[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)、 [**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)和**PoCallDriver**之前，必须调用**PoStartNextPowerIrp** 。 以其他顺序调用例程可能会导致系统死锁。

即使某个驱动程序失败了 IRP，它仍必须调用**PoStartNextPowerIrp**来通知电源管理器它已准备好处理其他电源 IRP。

以下各节阐明了每种类型的驱动程序应何时调用此例程：

[从筛选器驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-filter-driver.md)

[从设备电源策略所有者处调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-device-power-policy-owner.md)

[从总线驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-bus-driver.md)

 

 




