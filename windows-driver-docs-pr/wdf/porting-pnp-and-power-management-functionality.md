---
title: 移植 PnP 和电源管理
description: 移植 PnP 和电源管理
ms.assetid: 29ADD3CF-7CDE-4D97-8082-76B4F94DB6A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a9b8a68220e775e8992d2236ad7a95e407707be
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185195"
---
# <a name="porting-pnp-and-power-management"></a>移植 PnP 和电源管理


WDF 实现即插即用 (PnP) 和电源管理的智能默认值，因此包含大多数筛选器驱动程序的简单驱动程序 (，) 不需要其他代码即可满足 PnP 的基本要求。 框架自动创建和管理 PnP、电源管理和电源策略状态机。 默认情况下：

-   FDO 拥有设备的电源策略。
-   只需要 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调;所有其他 PnP 和电源管理回调都是可选的。 驱动程序实现其他回调以支持特定于设备的功能。
-   此框架实现了所有 WDFQUEUE 对象的电源管理，因此，仅当设备硬件可用时，默认情况下，请求才会从队列调度到驱动程序的 i/o 事件回调)  (。

如果设备不支持中断或映射内存，或者当发生电源转换时需要初始化或 deinitialization，则 WDF 驱动程序只需要 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调。
插入或删除设备时，框架按定义的顺序调用 PnP 和电源事件回调。 本节中的主题描述了 PDOs、FDOs 和 filter DOs 的顺序，这一点略有不同：

-   [函数或筛选器设备对象的幂序列](power-up-sequence-for-a-function-or-filter-driver.md)
-   [物理设备对象的通电顺序](power-up-sequence-for-a-bus-driver.md)
-   [函数或筛选器设备对象的电源和删除顺序](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [物理设备对象的电源和删除顺序](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [意外删除顺序](surprise-removal-sequence.md)

有关对应于每个次要 PnP 和电源 IRP 代码的回调的完整列表，请参阅 [WDM irp 和 WDF 事件回调函数](wdm-irps-and-kmdf-event-callback-functions.md)。

有关在基于框架的驱动程序中支持 PnP 和电源管理的详细信息，请参阅以下主题：

-   [支持在驱动程序中进行 PnP 和电源管理](supporting-pnp-and-power-management-in-your-driver.md)
-   [电源策略所有权](power-policy-ownership.md)

 

