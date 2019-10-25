---
title: WDI 选择性挂起功能注册
description: 下面是用于注册 USB 选择性挂起功能的流关系图。
ms.assetid: E4AE424F-2017-4111-B4C7-DF0BA6A40A15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85f29f6c50540707f1fe179c7ee51bc0981fcd9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842903"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI 选择性挂起功能注册


下面是用于注册 USB 选择性挂起功能的流关系图。

![wdi 选择性挂起功能注册](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap （PM （ss））、\*SelectiveSuspend、 **LeIdleNotificationHandler**和**LeCancelIdleNotificationHandler**必须为 TRUE 或有效，WDI 才能注册 WLAN 支持选择性挂起。

当 WDI 决定可以支持选择性挂起时，WDI 还会向 NDIS 注册一个可选的处理程序。

## <a name="related-topics"></a>相关主题


[*MiniportWdiCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

[*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

 

 






