---
title: 提供设备电池严重短缺通知
description: 提供设备电池严重短缺通知
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
ms.openlocfilehash: b4377456517a153610c7a88f66c7d5674a010309
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543396"
---
# <a name="supplying-battery-device-notification"></a>提供设备电池严重短缺通知


## <span id="ddk_supplying_battery_device_notification_dg"></span><span id="DDK_SUPPLYING_BATTERY_DEVICE_NOTIFICATION_DG"></span>


Miniclass 驱动程序负责监视它支持的电池的状态和通知重要发生更改时的类驱动程序。

除了[ *BatteryMiniQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff536274)例程，miniclass 驱动程序还提供[ *BatteryMiniSetStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536277)并[ *BatteryMiniDisableStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536272)例程。 类驱动程序将使用*BatteryMiniSetStatusNotify*并*BatteryMiniDisableStatusNotify*例程以请求和取消的特定电池状态通知。 这些例程与类和 miniclass 驱动程序状态例程中下一节所述进行交互。 有关这些两个 miniclass 例程的详细信息，请参阅[设置和取消电池严重短缺通知](setting-and-canceling-battery-notification.md)。

 

 




