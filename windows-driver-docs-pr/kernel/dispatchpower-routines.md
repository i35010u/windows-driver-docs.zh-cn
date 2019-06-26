---
title: DispatchPower 例程
description: DispatchPower 例程
ms.assetid: e385064f-cbdb-432f-951a-743217891333
keywords:
- 调度例程 WDK 内核，DispatchPower 例程
- DispatchPower 例程
- 电源管理 WDK 内核，调度例程
- IRP_MJ_POWER I/O 函数代码
- 可移动设备电源调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9567c377cfcbec6ea17da0eeccf80f3dbd594513
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384982"
---
# <a name="dispatchpower-routines"></a>DispatchPower 例程





驱动程序的[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程支持[电源管理](implementing-power-management.md)通过处理 Irp 为[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) I/O 函数代码。 与相关联**IRP\_MJ\_POWER**函数代码是电源管理的多个次要 I/O 函数代码。 电源管理器使用这些次要函数代码来指示驱动程序，以更改电源状态，以等待并响应系统唤醒事件和查询有关他们的设备的驱动程序。

每个驱动程序*DispatchPower*例程执行下列任务：

-   如有可能处理 IRP。

-   将 IRP 传递到设备中的下一个较低驱动程序堆栈，使用[ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)。

-   如果总线驱动程序，则执行请求的电源操作在设备上并完成 IRP。

设备的所有驱动程序必须有机会处理设备的 power Irp 除在少数情况下允许函数或筛选器驱动程序失败 IRP 的位置。 大多数函数和筛选器驱动程序执行一些处理，或者设置[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程的每个 power IRP，然后将向下一个较低的驱动程序 IRP 传递而未完成它。 最终 IRP 到达总线驱动程序，其中以物理方式根据需要更改设备的电源状态，完成 IRP。

当 IRP 已经完成时，I/O 管理器调用任何*IoCompletion*设置由驱动程序，如设备堆栈下的行程 IRP 的例程。 驱动程序是否需要设置完成例程取决于 IRP 和驱动程序的个人的要求的类型。

Power Irp 按设备堆栈 （基础总线驱动程序） 中的最低驱动程序，然后按每个连续的驱动程序堆栈，，必须首先处理打开设备的电源。 按设备堆栈顶部的驱动程序，然后按每个连续的驱动程序将在堆栈的下层，，必须首先处理关闭设备电源 power Irp。

### <a name="special-handling-for-removable-devices"></a>对可移动设备的特殊处理

在其*DispatchPower*例程，可移动设备的驱动程序应检查以查看设备是否仍然存在。 如果设备已被删除，则驱动程序不应将传递到下一个较低的驱动程序 IRP。 相反，该驱动程序应执行以下操作：

-   调用[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)以开始处理 IRP 的下一个幂。

-   设置**Irp-&gt;IoStatus.Status**于状态\_删除\_PENDING。

-   调用[ **IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)，指定 IO\_否\_增量，以完成 IRP。

-   返回状态\_删除\_PENDING。

 

 




