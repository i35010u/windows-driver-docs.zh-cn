---
title: 处理系统查询能耗 IRP 中一个筛选器或功能驱动程序
description: 处理系统查询能耗 IRP 中一个筛选器或功能驱动程序
ms.assetid: 81d921d5-6db8-4858-b86e-1484781faba5
keywords:
- 查询能耗 Irp WDK 电源管理
- 筛选器驱动程序 WDK 电源管理
- 功能的驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 691eeb9b34709a19c4405e40826b2f5fc348d915
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556084"
---
# <a name="handling-a-system-query-power-irp-in-a-filter-or-function-driver"></a>处理系统查询能耗 IRP 中一个筛选器或功能驱动程序





筛选器或函数的驱动程序 （这不是设备的电源策略所有者） 应传递一个系统查询能耗 IRP 到下一步低驱动程序，在以下步骤：

1.  调用[ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)，并传递当前 IRP，以确保该驱动程序不会接收即插即用[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求，而同时处理 IRP 的能力。

    如果**IoAcquireRemoveLock**返回失败状态，该驱动程序不应继续处理 IRP。 相反，从 Windows Vista 开始，驱动程序应调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成 IRP 并返回故障状态。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，该驱动程序应调用[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)，调用**IoCompleteRequest**完成 IRP，并返回失败状态。

2.  确定它是否应失败查询。 有关指南，请参阅[失败的系统查询能耗 IRP 中一个筛选器或功能驱动程序](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)和完成处理该部分中所述。

3.  调用[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅）

4.  设置 IRP 堆栈位置 ([**IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)或[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387))。 该驱动程序可以设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程中 IRP，但这样很少需要。

5.  调用**IoCallDriver** （在 Windows 7 和 Windows Vista） 或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) （在 Windows Server 2003、 Windows XP 和 Windows 2000） 以将 IRP 传递给下一个较低驱动程序。

6.  调用[ **IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)。 但是，如果该驱动程序设置*IoCompletion* IRP，例程进行此调用，从*IoCompletion*例程相反。

7.  返回状态\_PENDING 从其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

 

 




