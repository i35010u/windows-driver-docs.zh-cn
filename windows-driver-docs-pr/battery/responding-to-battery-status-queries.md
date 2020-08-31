---
title: 响应电池状态查询
description: 响应电池状态查询
ms.assetid: 756d7dd3-c4cc-4185-95cf-5a28ce86cacc
keywords:
- 电池状态 WDK
- 电池电量低 WDK
- 放电电池
- 电源状态 WDK 电池
- 故障电池 WDK
- 电池故障 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8edac1ccc956087e402d61a091ebc6b4823eb2f6
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056875"
---
# <a name="responding-to-battery-status-queries"></a>响应电池状态查询


## <span id="ddk_responding_to_battery_status_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_STATUS_QUERIES_DG"></span>


电池类驱动程序调用 miniclass 驱动程序的 [*BatteryMiniQueryStatus*](/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback) 例程，以获取电池的电源状态、容量、电压和放电速率。 下面是此例程的原型：

```cpp
typedef
NTSTATUS
(*BCLASS_QUERY_STATUS)(
    IN PVOID Context,
    IN ULONG BatteryTag,
    OUT PBATTERY_STATUS BatteryStatus
    );
```

*上下文*参数是指向上下文区域的指针，该上下文区域由 miniclass 驱动程序分配，并在设备初始化时在[**电池 \_ 微型端口 \_ 信息**](/windows/desktop/api/batclass/ns-batclass-battery_miniport_info)结构中传递给类驱动程序。 *BatteryTag*参数是之前由 BatteryMiniQueryTag 返回的值。

在 "缓冲电池 \_ 状态" 结构中，miniclass 驱动程序会根据 miniclass 驱动程序可以确定的范围，将电池的电压、容量和充电/放电速率报告给你。 Miniclass 驱动程序还报告以下一个或多个常量，用于描述电池的电源状况：

-   电池 \_ 充电

-   电池 \_ 放电

-   电池电量接通 \_ 电源 \_ \_

-   电池 \_ 严重

Miniclass 驱动程序不应报告极低、正在停止电池 (电池电量 \_ 严重短缺和电池 \_ 放电) ，直到已确定该条件不只是暂时性波动，并已用尽 remedying 这种情况。 例如，如果 miniclass 驱动程序可以切换到 AC 电源或其他电池，则此类补救措施可能包括切换到交流电源。

当 miniclass 驱动程序报告严重不足的电池电量时，电源管理器会假定电池故障即将用完。 如果电池提供系统电源，或者是辅助 (充电) 单元，则系统会针对严重电池执行 DC 电源策略。 电源策略的详细信息与系统不同，具体取决于硬件功能、应用程序设置和用户首选项。 通常，系统会尝试进入睡眠状态或关闭计算机。 有关详细信息，请参阅 [系统电源策略](../kernel/system-power-policy.md)。

类驱动程序的 [**BatteryClassStatusNotify**](/windows/desktop/api/batclass/nf-batclass-batteryclassstatusnotify) 例程和 miniclass 驱动程序的 [*BatteryMiniQueryStatus*](/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)、 [*BatteryMiniSetStatusNotify*](/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)和 [*BatteryMiniDisableStatusNotify*](/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback) 例程按两个驱动程序的顺序使用，以提供及时的状态信息。 有关详细信息，请参阅 [电池状态和通知例程的交互](interaction-of-battery-status-and-notification-routines.md)。

 

