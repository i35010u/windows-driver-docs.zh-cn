---
title: 使筛选器或函数驱动程序中的系统 Query-Power IRP 失败
description: 使筛选器或函数驱动程序中的系统 Query-Power IRP 失败
ms.assetid: 7c4ceb8e-94f4-4ff7-9d45-1094e9a861fd
keywords:
- 查询能耗 Irp WDK 电源管理
- 筛选器驱动程序 WDK 电源管理
- 功能的驱动程序 WDK 电源管理
- 失败查询能耗 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c453890a3f68b23cbf02d0ef7fd16fb9dd59684f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576054"
---
# <a name="failing-a-system-query-power-irp-in-a-filter-or-function-driver"></a>使筛选器或函数驱动程序中的系统 Query-Power IRP 失败





筛选器或函数的驱动程序 （这不是设备的电源策略所有者） 可能会失败[ **IRP\_MN\_查询\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)请求以下组件之一是否true:

-   该设备已启用的唤醒和请求的系统电源状态小于提供支持的值比[ **SystemWake**](systemwake.md)，它指定设备可以将系统唤醒从其提供最低支持的状态。 例如，可以从 s2 切换但不能从 S3 将系统唤醒的设备将适用于 S3 失败查询，但对 S2 成功查询。

-   输入与所请求的状态相对应的设备电源状态会强制驱动程序放弃可能会丢失数据，例如打开调制解调器连接的操作。 驱动程序很少会失败查询出于此原因;在大多数情况下，应用程序处理这种情况。

失败**IRP\_MN\_查询\_POWER**系统电源状态，驱动程序的请求应执行以下步骤：

1.  调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)以指示驱动程序已准备好处理 IRP 的下一个幂。 （Windows Server 2003、 Windows XP 和 Windows 2000 仅）

2.  设置**Irp-&gt;IoStatus.Status**为失败状态，并调用[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)，指定 IO\_否\_增量。 不要传递 IRP 进一步向下设备堆栈。

3.  调用[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)释放以前获取的锁。

4.  返回从故障状态及其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

 

 




