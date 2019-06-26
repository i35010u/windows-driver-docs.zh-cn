---
title: 避免 NDIS 电源管理问题
description: 避免 NDIS 电源管理问题
ms.assetid: 58bd91d5-68bd-471d-a961-6e0676d4a352
keywords:
- 电源管理 WDK NDIS 微型端口，问题
- 网络接口卡 WDK 网络、 电源问题
- Nic WDK 网络、 电源问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c218f5d28457c336a5ca24a5eaeecc8f7513fb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384408"
---
# <a name="avoiding-ndis-power-management-problems"></a>避免 NDIS 电源管理问题





以下规则将帮助你避免出现与网络适配器的电源管理问题：

-   网络适配器必须始终报告总线驱动程序对其电源管理功能。

-   不要尝试启用或禁用基于注册表设置的网络适配器的电源管理。 网络适配器的微型端口驱动程序初始化之前，NDIS 从总线驱动程序获取有关网络适配器的电源管理信息。 如果获取从总线驱动程序的信息指示网络适配器不是电源管理功能，NDIS 视为旧网络适配器的网络适配器和不会发出[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)到网络适配器的微型端口驱动程序的请求。

-   不要尝试提供用户界面中的自定义电源管理控件。

 

 





