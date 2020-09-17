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
ms.openlocfilehash: f3381b70d126d808df59fb748ee4fb8202ebe2b4
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716604"
---
# <a name="interaction-of-battery-status-and-notification-routines"></a>电池状态和通知例程的交互


## <span id="ddk_interaction_of_battery_status_and_notification_routines_dg"></span><span id="DDK_INTERACTION_OF_BATTERY_STATUS_AND_NOTIFICATION_ROUTINES_DG"></span>


类驱动程序可以请求和接收电池状态--miniclass 驱动程序可以通过几种方式提供电池状态。

如果 miniclass 驱动程序提供 [*BatteryMiniSetStatusNotify*](/windows/win32/api/batclass/nc-batclass-bclass_set_status_notify_callback) 例程，则可以注册类驱动程序，以便在电池容量超出指定范围或其电源状态更改时收到通知。 出现任何已注册的条件时，miniclass 驱动程序将调用 [**BatteryClassStatusNotify**](/windows/win32/api/batclass/nf-batclass-batteryclassstatusnotify)。

请注意， **BatteryClassStatusNotify** 不提供状态信息;其唯一参数是触发通知的电池的上下文。 它仅通知类驱动程序电池的状态已更改。 如果需要详细信息，类驱动程序将调用 [*BatteryMiniQueryStatus*](/windows/win32/api/batclass/nc-batclass-bclass_query_status_callback) 。

如果 miniclass 驱动程序不支持 *BatteryMiniSetStatusNotify*，则类驱动程序会通过定期调用 *BatteryMiniQueryStatus* 例程来轮询状态，但不常发生时间间隔。

与任何通知请求无关，miniclass 驱动程序必须在出现以下任何情况时调用 **BatteryClassStatusNotify** ：

-   电池处于联机或脱机状态。

-   电池容量严重不足。

-   电池的电源状态发生变化：它开始充电、开始放电、停止充电或停止放电。

在报告严重不足的电池放电之前，miniclass 驱动程序应尝试解决此问题，如前文所述的 [响应电池状态查询](responding-to-battery-status-queries.md)中所述。

 

