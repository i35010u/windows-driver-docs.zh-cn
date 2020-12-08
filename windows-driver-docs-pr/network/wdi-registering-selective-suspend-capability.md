---
title: WDI 选择性挂起功能注册
description: 下面是用于注册 USB 选择性挂起功能的流关系图。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4d787c09c6fe7bc0bfc4d5a5007a31d6cc528b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822089"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI 选择性挂起功能注册


下面是用于注册 USB 选择性挂起功能的流关系图。

![wdi 选择性挂起功能注册](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap (PM (ss) # A3、 \* SelectiveSuspend、 **LeIdleNotificationHandler** 和 **LeCancelIdleNotificationHandler** 必须为 true 或有效，WDI 才能注册 WLAN 支持选择性挂起。

当 WDI 决定可以支持选择性挂起时，WDI 还会向 NDIS 注册一个可选的处理程序。

## <a name="related-topics"></a>相关主题


[*MiniportWdiCancelIdleNotification*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

[*MiniportWdiIdleNotification*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

 

