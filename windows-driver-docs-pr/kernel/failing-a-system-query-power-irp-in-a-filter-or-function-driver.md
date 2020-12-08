---
title: 使筛选器或函数驱动程序中的系统 Query-Power IRP 失败
description: 使筛选器或函数驱动程序中的系统 Query-Power IRP 失败
keywords:
- 查询-power Irp WDK 电源管理
- 筛选器驱动程序 WDK 电源管理
- 函数驱动程序 WDK 电源管理
- 查询失败-power Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33cff100f729f3bfda194a4d01b16822c074ee60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793561"
---
# <a name="failing-a-system-query-power-irp-in-a-filter-or-function-driver"></a>使筛选器或函数驱动程序中的系统 Query-Power IRP 失败





如果满足以下任一条件，则不是设备的电源策略所有者 (筛选器或函数驱动程序) 可能会导致 [**IRP \_ MN \_ 查询 \_ 电源**](./irp-mn-query-power.md) 请求失败：

-   设备启用了唤醒，并且所请求的系统电源状态比 [**SystemWake**](systemwake.md)的值低，后者指定了设备可以唤醒系统的最小供电状态。 例如，可以从 S2 唤醒系统但不是从 S3 唤醒的设备会导致 S3 查询失败，但会成功查询 S2。

-   如果输入的设备电源状态与所请求的状态对应，则会强制驱动程序放弃会丢失数据的操作，如打开的调制解调器连接。 出于此原因，驱动程序很少导致查询失败;在大多数情况下，应用程序会处理这种情况。

若要使 **IRP \_ MN \_ 查询 \_ 电源** 状态请求失败，驱动程序应执行以下步骤：

1.  调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) ，以指示驱动程序已准备好处理下一个电源 IRP。 仅 (Windows Server 2003、Windows XP 和 Windows 2000) 

2.  将 **Irp- &gt; IoStatus** 设置为失败状态并调用 [**IOCOMPLETEREQUEST**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)，同时指定 IO \_ NO \_ 增量。 不要将 IRP 沿设备堆栈进一步向下传递。

3.  调用 [**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) 以释放以前获取的锁。

4.  从其 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程返回失败状态。

 

