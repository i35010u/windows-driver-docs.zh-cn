---
title: 提供电池设备通知
description: 提供电池设备通知
ms.assetid: 7104c43b-84f1-496d-9552-608101f5b379
keywords:
- 电池通知 WDK
- 电池 miniclass 驱动程序 WDK，通知
- 通知 WDK 电池
- 电池 miniclass 驱动程序 WDK，状态报告
- 状态信息 WDK 电池
- 监视电池状态
- 电池类驱动程序 WDK，通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d81f1495b4407cc923d0995a481605a84ec72ee3
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056851"
---
# <a name="supplying-battery-device-notification"></a>提供电池设备通知


## <span id="ddk_supplying_battery_device_notification_dg"></span><span id="DDK_SUPPLYING_BATTERY_DEVICE_NOTIFICATION_DG"></span>


Miniclass 驱动程序负责监视它所支持的电池的状态，并在发生重大更改时通知类驱动程序。

除了 [*BatteryMiniQueryStatus*](/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback) 例程以外，miniclass 驱动程序还提供 [*BatteryMiniSetStatusNotify*](/windows/desktop/api/batclass/nc-batclass-bclass_set_status_notify_callback) 和 [*BatteryMiniDisableStatusNotify*](/windows/desktop/api/batclass/nc-batclass-bclass_disable_status_notify_callback) 例程。 类驱动程序使用 *BatteryMiniSetStatusNotify* 和 *BatteryMiniDisableStatusNotify* 例程来请求和取消特定电池状态的通知。 这些例程与类和 miniclass 驱动程序状态例程交互，如下一节中所述。 有关这两个 miniclass 例程的详细信息，请参阅 [设置和取消电池通知](setting-and-canceling-battery-notification.md)。

 

