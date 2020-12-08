---
title: 电源管理的必需和可选 OID
description: 电源管理的必需和可选 OID
keywords:
- Oid WDK 网络，电源管理
- 唤醒功能，WDK 网络，Oid
- 电源管理 WDK NDIS 微型端口，Oid
- 对象标识符 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e56852db4916ea445741f97241f5c0661cab0c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797915"
---
# <a name="required-and-optional-oids-for-power-management"></a>电源管理的必需和可选 OID





对于微型端口驱动程序，支持电源管理需要支持 (Oid) 的电源管理对象标识符。 有关微型端口驱动程序如何处理查询并将其设置为 Oid 的详细说明，请参阅 [获取和 SettingMiniport 驱动程序信息和 WMI 对 WMI 的支持](ndis-management-information-and-oids.md)。

对于微型端口驱动程序有两个级别的电源管理支持：

1.  微型端口驱动程序可以支持在电源状态之间进行转换的网络适配器。 此支持是支持的最低级别。 有关网络适配器的设备电源状态的说明，请参阅 [网络适配器的设备电源状态](device-power-states-for-network-adapters.md)。

2.  微型端口驱动程序还可以支持一个或多个 [网络唤醒事件](network-wake-up-events.md)。

小型端口驱动程序在初始化期间报告电源管理功能。 有关在初始化期间报告的电源管理功能的详细信息，请参阅 [**NDIS \_ 微型端口 \_ 适配器 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes) 和相关的属性结构。

微型端口驱动程序必须直接支持或在网络适配器的属性中使用以下 Oid，才能在电源状态之间进行转换：

-   [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md)

    中间驱动程序必须响应此 OID 查询。 NDIS \_ \_ 代表物理网络适配器响应 OID PNP 功能请求。 有关在中间驱动程序中响应此 OID 的详细信息，请参阅 [在中间驱动程序中处理 PnP 事件和电源管理事件](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)。

-   [OID \_ PNP \_ 查询 \_ 能力](./oid-pnp-query-power.md)

    此 OID 指定网络适配器应准备转换的设备电源状态。 小型端口驱动程序必须始终返回 NDIS \_ 状态 \_ "成功" 以响应 OID \_ PNP 查询电源的查询 \_ \_ 。 通过返回 NDIS \_ 状态 "成功" 以 \_ 响应此 OID 请求，微型端口驱动程序保证在收到后续 OID \_ PNP \_ 设置电源请求时，它会将网络适配器转换为指定的设备电源状态 \_ 。 在这种情况下，微型端口驱动程序必须不执行任何操作来危害转换。

-   [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md)

    此 OID 指示网络适配器必须转换为指示的设备电源状态。 在驱动程序返回 NDIS 状态成功之前，微型端口驱动程序必须将网络适配器设置为指定的状态 \_ \_ 。 小型端口驱动程序必须始终为 \_ \_ 响应此 OID 返回 NDIS 状态成功。 如果 OID \_ PNP \_ SET \_ POWER 将网络适配器设置为工作电源状态，而微型端口驱动程序未能通过此 OID，NDIS 会假定设备处于不可恢复的状态。

若要支持网络唤醒事件，微型端口驱动程序还必须支持 [OID \_ PNP \_ ENABLE \_ 唤醒 \_ ](./oid-pnp-enable-wake-up.md) OID。 协议驱动程序和 NDIS 都使用此 OID 启用网络适配器的唤醒功能。 有关详细信息，请参阅 [启用 Wake-Up 事件](enabling-wake-up-events.md)。

若要支持网络唤醒帧 (参阅 [网络 Wake-Up 事件](network-wake-up-events.md)) ，微型端口驱动程序还必须支持与唤醒事件相关的以下 oid：

-   [OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](./oid-pnp-add-wake-up-pattern.md)

    协议驱动程序使用此 OID 将唤醒模式添加到网络适配器或微型端口驱动程序或两者维护的列表。

-   [OID \_ PNP \_ 删除 \_ 唤醒 \_ \_ 模式](./oid-pnp-remove-wake-up-pattern.md)

    协议驱动程序使用此 OID 删除以前通过 OID \_ PNP \_ 添加 \_ 唤醒 \_ 模式指定的唤醒模式 \_ 。

支持网络唤醒事件的 NDIS 微型端口驱动程序可以选择支持以下与唤醒事件相关的统计 Oid：

-   [OID \_ PNP \_ 唤醒 \_ \_ 错误](./oid-pnp-wake-up-error.md)

    协议驱动程序将查询此 OID，以确定微型端口驱动程序的网络适配器发出信号的虚假唤醒的数目。

-   [OID \_ PNP \_ 唤醒 \_ 正常 \_](./oid-pnp-wake-up-ok.md)

    协议驱动程序将查询此 OID，以确定微型端口驱动程序的网络适配器发出信号的有效唤醒的数目。

 

