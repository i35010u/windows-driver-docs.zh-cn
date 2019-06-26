---
title: 电池状态和通知例程的交互
description: 电池状态和通知例程的交互
ms.assetid: 1f9a3785-4ea4-4b56-bc66-247dfe222377
keywords:
- 电池通知 WDK
- 电池 miniclass 驱动程序 WDK，通知
- 通知 WDK 电池
- 电池类驱动程序 WDK，通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d12ac75e3f1de5695eae4bd79b43866f2c7e001
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354060"
---
# <a name="interaction-of-battery-status-and-notification-routines"></a>电池状态和通知例程的交互


## <span id="ddk_interaction_of_battery_status_and_notification_routines_dg"></span><span id="DDK_INTERACTION_OF_BATTERY_STATUS_AND_NOTIFICATION_ROUTINES_DG"></span>


在类驱动程序可以请求并接收电池状态-和 miniclass 驱动程序可以提供电池状态-几种方式。

如果 miniclass 驱动程序提供了[ *BatteryMiniSetStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)例程，类驱动程序可以注册或时，电池容量超过或低于指定的范围，通知其电源状态更改。 当发生任何已注册的情况时，miniclass 驱动程序会调用[ **BatteryClassStatusNotify**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassstatusnotify)。

请注意， **BatteryClassStatusNotify**不提供状态信息; 其唯一的参数是触发通知的电池的上下文。 它只是通知电池的状态已更改的类驱动程序。 反过来，在类驱动程序调用[ *BatteryMiniQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)是否需要详细信息。

如果 miniclass 驱动程序不支持*BatteryMiniSetStatusNotify*，在类驱动程序通过调用对状态轮询*BatteryMiniQueryStatus*例程在正则但很少发生的时间间隔。

独立于任何通知的请求时，miniclass 驱动程序必须调用**BatteryClassStatusNotify**每当发生的以下任何一个：

-   电池将联机或脱机。

-   电池电量变得严重不足。

-   电池更改电源状态： 启动充电、 放电将启动、 停止充电时，或停止放电。

报告严重不足、 放电电池之前, miniclass 驱动程序应尝试解决该问题，如前面所述[响应的电池状态查询](responding-to-battery-status-queries.md)。

 

 




