---
title: WDI 选择性挂起功能注册
description: 下面是用于注册 USB 选择性挂起功能的流关系图。
ms.assetid: E4AE424F-2017-4111-B4C7-DF0BA6A40A15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72b9b609ffc5b2eeba8462adc426c9069ee5a9dd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213153"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI 选择性挂起功能注册


下面是用于注册 USB 选择性挂起功能的流关系图。

![wdi 选择性挂起功能注册](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap (PM (ss) # A3、 \* SelectiveSuspend、 **LeIdleNotificationHandler**和 **LeCancelIdleNotificationHandler** 必须为 true 或有效，WDI 才能注册 WLAN 支持选择性挂起。

当 WDI 决定可以支持选择性挂起时，WDI 还会向 NDIS 注册一个可选的处理程序。

## <a name="related-topics"></a>相关主题


[*MiniportWdiCancelIdleNotification*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

[*MiniportWdiIdleNotification*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

 

