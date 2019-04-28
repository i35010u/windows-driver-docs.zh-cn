---
title: 电源管理（NDIS 6.0 和 NDIS 6.1）
description: 电源管理（NDIS 6.0 和 NDIS 6.1）
ms.assetid: 10CACB4E-BBC8-497F-9B54-810518B726A8
keywords:
- 微型端口驱动程序 WDK 网络、 电源管理
- NDIS 微型端口驱动程序 WDK、 电源管理
- 电源管理 WDK 网络，微型端口驱动程序
- 电源管理 WDK NDIS 微型端口
- 电源管理 WDK NDIS 微型端口，有关微型端口驱动程序电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e386c5e8f29eb9ef099686979b27964badfb749
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342958"
---
# <a name="power-management-ndis-60-and-ndis-61"></a>电源管理（NDIS 6.0 和 NDIS 6.1）





本部分介绍引入了 Windows XP 和 NDIS 5.1 NDIS 电源管理接口。 此电源管理接口支持以下版本的 NDIS 中：

-   NDIS 5.1 (Windows XP)

-   NDIS 6.0 和更高版本的 NDIS （Windows Vista 和更高版本的 Windows）

本部分介绍：

-   NDIS 提供 NDIS 微型端口驱动程序的电源管理服务。

-   微型端口驱动程序要求，以支持电源管理。

-   如何 NDIS 电源策略设置的网络适配器。

本部分包括以下主题：

[电源管理的必需和可选的 Oid](required-and-optional-oids-for-power-management.md)

[适用于网络适配器的设备的电源状态](device-power-states-for-network-adapters.md)

[网络唤醒事件](network-wake-up-events.md)

[处理 OID\_PNP\_查询\_POWER OID](handling-an-oid-pnp-query-power-oid.md)

[处理 OID\_PNP\_设置\_POWER OID](handling-an-oid-pnp-set-power-oid.md)

[千兆位以太网网络适配器的电源管理注意事项](power-management-considerations-for-gigabit-ethernet-network-adapters.md)

[旧微型端口驱动程序的电源管理](power-management-for-old-miniport-drivers.md)

[NDIS 网络适配器设置电源策略的方式](how-ndis-sets-the-power-policy-for-a-network-adapter.md)

[避免 NDIS 电源管理问题](avoiding-ndis-power-management-problems.md)

**请注意**  从 NDIS 6.20 开始，NDIS 电源管理界面已进行了修订并扩展。 如果你正在开发支持电源管理的 NDIS 6.20 微型端口驱动程序，请查看中的信息[（NDIS 6.20 和更高版本） 的电源管理](https://msdn.microsoft.com/library/windows/hardware/hh205401)。 如果你正在开发支持电源管理的 NDIS 6.30 微型端口驱动程序，请查看中的信息[（NDIS 6.30 和更高版本） 的电源管理](https://msdn.microsoft.com/library/windows/hardware/hh440160)。

 

 

 





