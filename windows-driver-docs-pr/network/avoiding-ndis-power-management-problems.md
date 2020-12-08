---
title: 避免 NDIS 电源管理问题
description: 避免 NDIS 电源管理问题
keywords:
- 电源管理 WDK NDIS 微型端口，问题
- 网络接口卡 WDK 网络，电源问题
- Nic WDK 网络，电源问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dad3b7eaf50d4f78647cf2fccd1cd9cf5c2aa87b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813053"
---
# <a name="avoiding-ndis-power-management-problems"></a>避免 NDIS 电源管理问题





以下规则将帮助你避免网络适配器的电源管理问题：

-   网络适配器必须始终向总线驱动程序报告其电源管理功能。

-   不要尝试基于注册表设置来启用或禁用网络适配器的电源管理。 在初始化网络适配器的微型端口驱动程序之前，NDIS 从总线驱动程序获取有关网络适配器的电源管理信息。 如果从总线驱动程序获取的信息指示网络适配器不支持电源管理，NDIS 会将网络适配器视为旧的网络适配器，并且不会向网络适配器的微型端口驱动程序颁发 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md) 请求。

-   不要尝试在用户界面中提供自定义电源管理控件。

 

