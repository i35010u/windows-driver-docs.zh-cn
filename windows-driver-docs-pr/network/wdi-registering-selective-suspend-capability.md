---
title: WDI 选择性挂起功能注册
description: 下面是用于注册 USB 选择性挂起功能流关系图。
ms.assetid: E4AE424F-2017-4111-B4C7-DF0BA6A40A15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a94fb85f459820e5b0f250e4be2ba443e4deae7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548128"
---
# <a name="wdi-selective-suspend-capability-registration"></a>WDI 选择性挂起功能注册


下面是用于注册 USB 选择性挂起功能流关系图。

![wdi 选择性挂起功能注册](images/wdi-register-usb-selective-suspend-flow.png)

AdapterCap(PM(ss))， \*SelectiveSuspend， **LeIdleNotificationHandler**，和**LeCancelIdleNotificationHandler**必须为 true 或 WDI 中以注册 WLAN 支持选择性的有效挂起。

WDI 决定可以支持选择性挂起，WDI 还会注册到 NDIS 的可选处理程序。

## <a name="related-topics"></a>相关主题


[*MiniportWdiCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297560)

[*MiniportWdiIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297563)

 

 






