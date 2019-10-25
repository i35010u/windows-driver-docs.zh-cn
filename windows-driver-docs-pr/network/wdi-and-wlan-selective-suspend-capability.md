---
title: WDI 和 WLAN 选择性挂起功能
description: 本部分介绍如何为 WDI 驱动程序启用 USB 选择性挂起支持
ms.assetid: 4FCF726B-4CCF-4F0F-9088-2EABA0DA7D3C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 516723b367dbc1e311439fe191e970262fa4dde6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842934"
---
# <a name="wdi-and-wlan-selective-suspend-capability"></a>WDI 和 WLAN 选择性挂起功能


若要启用 USB 选择性挂起支持，LE 必须报告该功能。 NDIS 为此功能定义关键字。 有关详细信息，请参阅[用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

-   \*SelectiveSuspend： {Enable，Disable}

-   \*SSIdleTimeout：空闲超时（秒）

WDI 基于以下来源启用支持。

-   设备 INF：这会写入到设备安装程序中的下一项（从上面的关键字开始）。
-   注册表设置：此设置是从 INF 或设备的高级属性表中设置的，设备管理器中。
-   从 OID 返回的电源管理功能[\_WDI\_获取\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)。
-   NDIS 中的空闲处理程序[ **\_微型端口\_驱动程序\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)。
    -   [*MiniportWdiIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_idle_notification)

    -   [*MiniportWdiCancelIdleNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_cancel_idle_notification)

WDI 驱动程序为 LE 公开两个回调函数。

-   [**IdleNotificationComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_complete)

-   [**IdleNotificationConfirm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_idle_notification_confirm)

 

 





