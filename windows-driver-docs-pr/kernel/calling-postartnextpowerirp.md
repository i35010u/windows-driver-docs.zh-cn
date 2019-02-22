---
title: Calling PoStartNextPowerIrp
description: Calling PoStartNextPowerIrp
ms.assetid: 8b3fb578-2ac2-4a04-ac99-1cfd51b07b01
keywords:
- power Irp WDK 内核 PoStartNextPowerIrp
- PoStartNextPowerIrp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa55bfc81e8c8ebf9182c8a527c1e4ecacb305c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543894"
---
# <a name="calling-postartnextpowerirp"></a>Calling PoStartNextPowerIrp





使用 Windows Vista 开始，调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)不是必需的和对此例程的调用会执行任何电源管理操作。 但是，在 Windows Server 2003、 Windows XP 和 Windows 2000 中，查询能耗 IRP 或集 power IRP，驱动程序进行处理后，驱动程序必须调用**PoStartNextPowerIrp**以通知它已准备好接收另一种电源管理器IRP 的电源。 驱动程序必须调用**PoStartNextPowerIrp** IRP 时堆栈位置点到当前驱动程序，然后再调用[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)。

驱动程序必须为每一次调用此例程[ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)或[ **IRP\_MN\_设置\_电源**](https://msdn.microsoft.com/library/windows/hardware/ff551744)它收到的请求。 驱动程序不需要调用**PoStartNextPowerIrp**处理时[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)或[**IRP\_MN\_POWER\_序列**](https://msdn.microsoft.com/library/windows/hardware/ff551644)请求。

当驱动程序调用**PoStartNextPowerIrp**，当前的 IRP 堆栈位置必须指向当前驱动程序。 作为一般规则，此调用最好从进行[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。 **PoStartNextPowerIrp**前必须调用[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)， [ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)，并**PoCallDriver**。 调用例程的其他顺序可能会导致系统死锁。

即使驱动程序出现故障 IRP，不过必须调用**PoStartNextPowerIrp**以通知它已准备好处理另一个 power IRP 电源管理器。

以下部分阐明每种类型的驱动程序应调用此例程的时间：

[从筛选器驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-filter-driver.md)

[从设备电源策略所有者调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-device-power-policy-owner.md)

[从总线驱动程序调用 PoStartNextPowerIrp](calling-postartnextpowerirp-from-a-bus-driver.md)

 

 




