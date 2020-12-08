---
title: WDI 和 WLAN 选择性挂起功能
description: 本部分介绍如何为 WDI 驱动程序启用 USB 选择性挂起支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed5e9adde93ef351d467234f569db82d1db9ed99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837895"
---
# <a name="wdi-and-wlan-selective-suspend-capability"></a>WDI 和 WLAN 选择性挂起功能


若要启用 USB 选择性挂起支持，LE 必须报告该功能。 NDIS 为此功能定义关键字。 有关详细信息，请参阅 [用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

-   \*SelectiveSuspend： {Enable，Disable}

-   \*SSIdleTimeout：空闲超时（秒）

WDI 基于以下来源启用支持。

-   设备 INF：这会写入到设备安装程序中的下一项（从上面的关键字开始）。
-   注册表设置：此设置是从 INF 或设备的高级属性表中设置的，设备管理器中。
-   从 OID 返回的电源管理功能 [ \_ WDI \_ 获取 \_ 适配器 \_ 功能](./oid-wdi-get-adapter-capabilities.md)。
-   [**NDIS \_ 微型端口 \_ 驱动程序 \_ WDI \_ 特征**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)中的空闲处理程序。
    -   [*MiniportWdiIdleNotification*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

    -   [*MiniportWdiCancelIdleNotification*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

WDI 驱动程序为 LE 公开两个回调函数。

-   [**IdleNotificationComplete**](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_complete)

-   [**IdleNotificationConfirm**](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_confirm)

 

