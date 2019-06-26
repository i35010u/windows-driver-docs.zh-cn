---
title: WDI 选择性挂起功能注册
description: 下面是用于注册 USB 选择性挂起功能流关系图。
ms.assetid: E4AE424F-2017-4111-B4C7-DF0BA6A40A15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5108c11e1832033fda4c92de96e0581a1c4cdc7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384348"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI 选择性挂起功能注册


下面是用于注册 USB 选择性挂起功能流关系图。

![wdi 选择性挂起功能注册](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap(PM(ss))， \*SelectiveSuspend， **LeIdleNotificationHandler**，和**LeCancelIdleNotificationHandler**必须为 true 或 WDI 中以注册 WLAN 支持选择性的有效挂起。

WDI 决定可以支持选择性挂起，WDI 还会注册到 NDIS 的可选处理程序。

## <a name="related-topics"></a>相关主题


[*MiniportWdiCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

 

 






