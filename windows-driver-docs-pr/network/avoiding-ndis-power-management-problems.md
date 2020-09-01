---
title: 避免 NDIS 电源管理问题
description: 避免 NDIS 电源管理问题
ms.assetid: 58bd91d5-68bd-471d-a961-6e0676d4a352
keywords:
- 电源管理 WDK NDIS 微型端口，问题
- 网络接口卡 WDK 网络，电源问题
- Nic WDK 网络，电源问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ec429d952a15f3391b7cd88321960150e7484fc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215973"
---
# <a name="avoiding-ndis-power-management-problems"></a>避免 NDIS 电源管理问题





以下规则将帮助你避免网络适配器的电源管理问题：

-   网络适配器必须始终向总线驱动程序报告其电源管理功能。

-   不要尝试基于注册表设置来启用或禁用网络适配器的电源管理。 在初始化网络适配器的微型端口驱动程序之前，NDIS 从总线驱动程序获取有关网络适配器的电源管理信息。 如果从总线驱动程序获取的信息指示网络适配器不支持电源管理，NDIS 会将网络适配器视为旧的网络适配器，并且不会向网络适配器的微型端口驱动程序颁发 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md) 请求。

-   不要尝试在用户界面中提供自定义电源管理控件。

 

