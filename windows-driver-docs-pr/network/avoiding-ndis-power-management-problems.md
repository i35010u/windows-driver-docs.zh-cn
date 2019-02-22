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
ms.openlocfilehash: fbe1e28f0b61cf833cae2e14fdc48519fab449cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554979"
---
# <a name="avoiding-ndis-power-management-problems"></a>避免 NDIS 电源管理问题





以下规则将帮助你避免出现与网络适配器的电源管理问题：

-   网络适配器必须始终报告总线驱动程序对其电源管理功能。

-   不要尝试启用或禁用基于注册表设置的网络适配器的电源管理。 网络适配器的微型端口驱动程序初始化之前，NDIS 从总线驱动程序获取有关网络适配器的电源管理信息。 如果获取从总线驱动程序的信息指示网络适配器不是电源管理功能，NDIS 视为旧网络适配器的网络适配器和不会发出[OID\_PNP\_功能](https://msdn.microsoft.com/library/windows/hardware/ff569774)到网络适配器的微型端口驱动程序的请求。

-   不要尝试提供用户界面中的自定义电源管理控件。

 

 





