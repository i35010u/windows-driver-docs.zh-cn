---
title: WDI 和 WLAN 选择性挂起功能
description: 本部分介绍如何启用 USB 选择性挂起 WDI 驱动程序的支持
ms.assetid: 4FCF726B-4CCF-4F0F-9088-2EABA0DA7D3C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2c250d0be241b1f12e69199cf92cf082168bd48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522800"
---
# <a name="wdi-and-wlan-selective-suspend-capability"></a>WDI 和 WLAN 选择性挂起功能


若要启用 USB 选择性挂起支持，LE 必须报告功能。 NDIS 定义此功能的关键字。 有关详细信息，请参阅[NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

-   \*SelectiveSuspend: {启用、 禁用}

-   \*SSIdleTimeout： 空闲超时 （秒）

WDI 能够进行基于以下源的支持。

-   设备 INF:这是写入到在设备安装程序的下一项从上述的关键字。
-   注册表设置：此值设置从 INF 或设备在设备管理器的高级的属性表。
-   电源管理功能中的返回[OID\_WDI\_获取\_适配器\_功能](https://msdn.microsoft.com/library/windows/hardware/dn925838)。
-   空闲处理程序中的[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://msdn.microsoft.com/library/windows/hardware/mt297617)。
    -   [*MiniportWdiIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297563)

    -   [*MiniportWdiCancelIdleNotification*](https://msdn.microsoft.com/library/windows/hardware/mt297560)

WDI 驱动程序针对 LE 公开两个回调函数。

-   [**IdleNotificationComplete**](https://msdn.microsoft.com/library/windows/hardware/mt297600)

-   [**IdleNotificationConfirm**](https://msdn.microsoft.com/library/windows/hardware/mt297601)

 

 





