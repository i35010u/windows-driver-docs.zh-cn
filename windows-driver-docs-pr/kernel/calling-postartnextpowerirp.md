---
title: 调用 PoStartNextPowerIrp
description: 调用 PoStartNextPowerIrp
ms.assetid: 8b3fb578-2ac2-4a04-ac99-1cfd51b07b01
keywords:
- power Irp WDK 内核，PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36c2b12e6bcf21253f82e78cf00647178013048b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188639"
---
# <a name="calling-postartnextpowerirp"></a>调用 PoStartNextPowerIrp





从 Windows Vista 开始，调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) 不是必需的，并且调用此例程不会执行任何电源管理操作。 但是，在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序在处理查询-power IRP 或集电源 IRP 之后，必须调用 **PoStartNextPowerIrp** 来通知电源管理器它已准备好接收另一个 power IRP。 当 IRP 堆栈位置指向当前驱动程序并在调用[**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)之前，驱动程序必须调用**PoStartNextPowerIrp** 。

驱动程序必须为每个 [**IRP \_ MN \_ QUERY \_ power**](./irp-mn-query-power.md) 或 [**irp \_ MN \_ 设置 \_ **](./irp-mn-set-power.md) 其收到的 power request 调用此例程一次。 处理[**IRP \_ MN \_ WAIT \_ 唤醒**](./irp-mn-wait-wake.md)或[**irp \_ MN \_ 电源 \_ 序列**](./irp-mn-power-sequence.md)请求时，驱动程序不需要调用**PoStartNextPowerIrp** 。

当驱动程序调用 **PoStartNextPowerIrp**时，当前 IRP 堆栈位置必须指向当前驱动程序。 作为一般规则，此调用最好是从 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程进行。 在[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)、 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md)和**PoCallDriver**之前，必须调用**PoStartNextPowerIrp** 。 以其他顺序调用例程可能会导致系统死锁。

即使某个驱动程序失败了 IRP，它仍必须调用 **PoStartNextPowerIrp** 来通知电源管理器它已准备好处理其他电源 IRP。

以下各节阐明了每种类型的驱动程序应何时调用此例程：

[从筛选器驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-filter-driver.md)

[从设备电源策略所有者调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-device-power-policy-owner.md)

[从总线驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-bus-driver.md)

 

