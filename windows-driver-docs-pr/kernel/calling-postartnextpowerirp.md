---
title: 调用 PoStartNextPowerIrp
description: 调用 PoStartNextPowerIrp
ms.assetid: 8b3fb578-2ac2-4a04-ac99-1cfd51b07b01
keywords:
- power Irp WDK 内核 PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f1e9f36d60ede49f55579bc8eab1224e647bae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385262"
---
# <a name="calling-postartnextpowerirp"></a>调用 PoStartNextPowerIrp





使用 Windows Vista 开始，调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)不是必需的和对此例程的调用会执行任何电源管理操作。 但是，在 Windows Server 2003、 Windows XP 和 Windows 2000 中，查询能耗 IRP 或集 power IRP，驱动程序进行处理后，驱动程序必须调用**PoStartNextPowerIrp**以通知它已准备好接收另一种电源管理器IRP 的电源。 驱动程序必须调用**PoStartNextPowerIrp** IRP 时堆栈位置点到当前驱动程序，然后再调用[ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)。

驱动程序必须为每一次调用此例程[ **IRP\_MN\_查询\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)或[ **IRP\_MN\_设置\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)它收到的请求。 驱动程序不需要调用**PoStartNextPowerIrp**处理时[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)或[**IRP\_MN\_POWER\_序列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence)请求。

当驱动程序调用**PoStartNextPowerIrp**，当前的 IRP 堆栈位置必须指向当前驱动程序。 作为一般规则，此调用最好从进行[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程。 **PoStartNextPowerIrp**前必须调用[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)， [ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，并**PoCallDriver**。 调用例程的其他顺序可能会导致系统死锁。

即使驱动程序出现故障 IRP，不过必须调用**PoStartNextPowerIrp**以通知它已准备好处理另一个 power IRP 电源管理器。

以下部分阐明每种类型的驱动程序应调用此例程的时间：

[从筛选器驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-filter-driver.md)

[从设备电源策略所有者调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-device-power-policy-owner.md)

[从总线驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-bus-driver.md)

 

 




