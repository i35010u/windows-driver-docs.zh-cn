---
title: 报告当系统回到 S0 状态时设备开机
description: 报告当系统回到 S0 状态时设备开机
ms.assetid: 35A48B37-8000-45DC-8E39-4B58ABE7DE68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e458da3c929727fb0c15704e62cdb3bc13f11456
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576637"
---
# <a name="reporting-device-powered-on-when-system-returns-to-s0"></a>报告当系统回到 S0 状态时设备开机


\[仅适用于 KMDF\]

PnP 管理器时系统将从低功耗状态恢复为其工作 (S0) 状态，将系统集-开启 IRP 发送 ([**IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)) 返回设备连接到其工作 (D0) 状态。 WDF 处理系统集 power IRP。 但是，由于多组件的方案中，驱动程序具有直接注册到电源管理框架 (PoFx)，该驱动程序必须调用[ **PoFxReportDevicePoweredOn** ](https://msdn.microsoft.com/library/windows/hardware/hh439526)时该设备已完成转换到其完全开启 (D0) 电源状态。 该驱动程序可以实现此目的通过注册 WDM 预处理例程时接收通知系统集 power IRP 到达。

该驱动程序可以使用以下过程：

1.  调用[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043)注册[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)回调函数[ **IRP\_MN\_设置\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)。 在回调中，该驱动程序中设置一个标志以指示它需要调用其设备扩展[ **PoFxReportDevicePoweredOn** ](https://msdn.microsoft.com/library/windows/hardware/hh439526)从其下一步[ *EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)回调。
2.  在中[ *EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)，则该标志是集、 驱动程序清除标志以及调用[ **PoFxReportDevicePoweredOn**](https://msdn.microsoft.com/library/windows/hardware/hh439526)。
3.  该驱动程序还检查的标志[ *EvtDeviceSelfManagedIoFlush*](https://msdn.microsoft.com/library/windows/hardware/ff540901)。 如果设置了标志，该设备无法返回到 D0 和删除设备。 在这种情况下，驱动程序调用[ **PoFxReportDevicePoweredOn** ](https://msdn.microsoft.com/library/windows/hardware/hh439526) ，然后注销与电源框架。

 

 





