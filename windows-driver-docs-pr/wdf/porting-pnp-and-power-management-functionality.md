---
title: 移植 PnP 和电源管理
description: 移植 PnP 和电源管理
ms.assetid: 29ADD3CF-7CDE-4D97-8082-76B4F94DB6A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f92630b67187ea7d63e65479e8e3dca501eb096
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379637"
---
# <a name="porting-pnp-and-power-management"></a>移植 PnP 和电源管理


WDF 实现插即用 (PnP) 和电源管理的智能默认值，因此简单驱动程序 （包括大多数筛选器驱动程序） 不需要附加代码以满足基本要求的即插即用。 该框架会自动创建和管理即插即用、 电源管理和电源策略状态机。 默认情况下：

-   FDO 拥有设备的电源策略。
-   仅[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) callback 是必需的; 所有其他 PnP 和电源管理回调是可选的。 驱动程序实现其他回调，以支持特定于设备的功能。
-   该框架实现电源管理的所有 WDFQUEUE 对象，以便默认情况下请求调度从队列到驱动程序的 I/O 事件回叫仅当设备硬件可用时 （即，在 D0 状态）。

如果设备不支持中断或映射内存，或不需要初始化或未初始化 power 转换发生时，仅要求 WDF 驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调。
当插入或删除设备时，框架将调用中定义的顺序的即插即用和电源事件回调。 在本部分中的主题介绍的个 PDOs，FDOs，都略有不同的顺序，并筛选 DOs:

-   [为实现功能或筛选设备对象的增益道具序列](power-up-sequence-for-a-function-or-filter-driver.md)
-   [物理设备对象的增益道具序列](power-up-sequence-for-a-bus-driver.md)
-   [电源关闭和删除序列的函数或筛选设备对象](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [电源关闭和删除序列物理设备对象](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [意外删除序列](surprise-removal-sequence.md)

对应于每个次要的即插即用和电源 IRP 代码的回调的完整列表，请参阅[WDM Irp 和 WDF 事件回调函数](wdm-irps-and-kmdf-event-callback-functions.md)。

有关支持即插即用和基于 framework 的驱动程序中的电源管理的详细信息，请参阅以下主题：

-   [在您的驱动程序支持的即插即用和电源管理](supporting-pnp-and-power-management-in-your-driver.md)
-   [电源策略所有权](power-policy-ownership.md)

 

 





