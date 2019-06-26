---
title: 提供电池设备通知
description: 提供电池设备通知
ms.assetid: 7104c43b-84f1-496d-9552-608101f5b379
keywords:
- 电池通知 WDK
- 电池 miniclass 驱动程序 WDK，通知
- 通知 WDK 电池
- 电池 miniclass 驱动程序 WDK，状态报告
- WDK 电池的状态信息
- 监视电池状态
- 电池类驱动程序 WDK，通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a97ace9e4f96bcf80f4dfec2dc5279e555fb8ca7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364715"
---
# <a name="supplying-battery-device-notification"></a>提供电池设备通知


## <span id="ddk_supplying_battery_device_notification_dg"></span><span id="DDK_SUPPLYING_BATTERY_DEVICE_NOTIFICATION_DG"></span>


Miniclass 驱动程序负责监视它支持的电池的状态和通知重要发生更改时的类驱动程序。

除了[ *BatteryMiniQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)例程，miniclass 驱动程序还提供[ *BatteryMiniSetStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback)并[ *BatteryMiniDisableStatusNotify* ](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback)例程。 类驱动程序将使用*BatteryMiniSetStatusNotify*并*BatteryMiniDisableStatusNotify*例程以请求和取消的特定电池状态通知。 这些例程与类和 miniclass 驱动程序状态例程中下一节所述进行交互。 有关这些两个 miniclass 例程的详细信息，请参阅[设置和取消电池严重短缺通知](setting-and-canceling-battery-notification.md)。

 

 




