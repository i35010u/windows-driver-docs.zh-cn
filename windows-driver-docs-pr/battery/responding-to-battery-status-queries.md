---
title: 响应电池状态查询
description: 响应电池状态查询
ms.assetid: 756d7dd3-c4cc-4185-95cf-5a28ce86cacc
keywords:
- 电池状态 WDK
- 低电池 WDK
- 放电电池 WDK
- 电源状态 WDK 电池
- 失败的电池 WDK
- 电池故障 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9f161b24ffa361a0ca63cb6b3a320c03aadf09b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364739"
---
# <a name="responding-to-battery-status-queries"></a>响应电池状态查询


## <span id="ddk_responding_to_battery_status_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_STATUS_QUERIES_DG"></span>


电池类驱动程序调用 miniclass 驱动[ *BatteryMiniQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)例程，以获取电源状态、 容量、 电压和出院事项电池的速率。 下面是此例程的原型：

```cpp
typedef
NTSTATUS
(*BCLASS_QUERY_STATUS)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    OUT PBATTERY_STATUS BatteryStatus
    );
```

*上下文*参数是指向 miniclass 驱动程序分配和传递给的类驱动程序中的上下文区域[**电池\_微型端口\_信息**](https://docs.microsoft.com/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)在设备初始化结构。 *BatteryTag*参数是 BatteryMiniQueryTag 以前返回的值。

在缓冲电池\_电池的电压、 容量和费用/放电速率的范围内 miniclass 驱动程序可以确定其状态结构 miniclass 驱动程序报告。 Miniclass 驱动程序还会报告一个或多个描述电池电源条件的以下常量：

-   电池\_正在充电

-   电池\_DISCHARGING

-   电池\_电源\_ON\_行

-   电池\_严重

Miniclass 驱动程序不应报告严重不足、 放电电池 (电池\_关键和电池\_DISCHARGING) 直到它具有已确定的条件不是只是暂时性的波动以及已经用完了所有其他纠正这种情况的方法。 这种补救措施可能包括切换到 AC 电源或另一个电池，如果 miniclass 驱动程序可以执行此操作。

当 miniclass 驱动程序报告严重不足、 放电电池时，电源管理器将假定即将发生电池故障时。 如果电池提供系统电源或是次要的 （可再充电） 单元格，系统将执行电池电量严重短缺的 DC 电源策略。 电源策略的详细信息的硬件功能、 应用程序设置和用户首选项而异系统之间。 通常情况下，系统会尝试输入睡眠状态或关闭计算机。 有关详细信息，请参阅[系统电源策略](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-policy)。

在类驱动程序[ **BatteryClassStatusNotify** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassstatusnotify)例程和 miniclass 驱动程序[ *BatteryMiniQueryStatus*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)， [ *BatteryMiniSetStatusNotify*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)，并[ *BatteryMiniDisableStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)例程在序列中使用由两个驱动程序若要提供及时的状态信息。 有关详细信息，请参阅[电池状态交互和通知例程](interaction-of-battery-status-and-notification-routines.md)。

 

 




