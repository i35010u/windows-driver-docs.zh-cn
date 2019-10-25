---
title: 电源管理的必需和可选 OID
description: 电源管理的必需和可选 OID
ms.assetid: 147e35b2-dfa5-4238-82e6-5c48ffa30af5
keywords:
- Oid WDK 网络，电源管理
- 唤醒功能，WDK 网络，Oid
- 电源管理 WDK NDIS 微型端口，Oid
- 对象标识符 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad88bdb5161051bb3137f62377ae148ec6aa62e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842031"
---
# <a name="required-and-optional-oids-for-power-management"></a>电源管理的必需和可选 OID





对于微型端口驱动程序，支持电源管理需要支持电源管理对象标识符（Oid）。 有关微型端口驱动程序如何处理查询并将其设置为 Oid 的详细说明，请参阅[获取和 SettingMiniport 驱动程序信息和 WMI 对 WMI 的支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

对于微型端口驱动程序有两个级别的电源管理支持：

1.  微型端口驱动程序可以支持在电源状态之间进行转换的网络适配器。 此支持是支持的最低级别。 有关网络适配器的设备电源状态的说明，请参阅[网络适配器的设备电源状态](device-power-states-for-network-adapters.md)。

2.  微型端口驱动程序还可以支持一个或多个[网络唤醒事件](network-wake-up-events.md)。

小型端口驱动程序在初始化期间报告电源管理功能。 有关在初始化期间报告的电源管理功能的详细信息，请参阅[**NDIS\_微型端口\_适配器\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)和相关的属性结构。

微型端口驱动程序必须直接支持或在网络适配器的属性中使用以下 Oid，才能在电源状态之间进行转换：

-   [OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)

    中间驱动程序必须响应此 OID 查询。 NDIS 响应 OID\_PNP\_功能请求代表物理网络适配器。 有关在中间驱动程序中响应此 OID 的详细信息，请参阅[在中间驱动程序中处理 PnP 事件和电源管理事件](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)。

-   [OID\_PNP\_QUERY\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)

    此 OID 指定网络适配器应准备转换的设备电源状态。 小型端口驱动程序必须始终将 NDIS\_\_状态返回为响应 OID\_PNP\_查询\_幂的查询。 通过返回 NDIS\_状态\_"成功" 响应此 OID 请求，微型端口驱动程序保证在收到后续 OID\_PNP\_集时，它会将网络适配器转换为指定的设备电源状态\_POWER request。 在这种情况下，微型端口驱动程序必须不执行任何操作来危害转换。

-   [OID\_PNP\_集\_电源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

    此 OID 指示网络适配器必须转换为指示的设备电源状态。 小型端口驱动程序必须将网络适配器设置为指定状态，然后驱动程序才会将 NDIS\_状态返回\_成功。 小型端口驱动程序必须始终将 NDIS\_状态返回为响应此 OID\_成功。 如果 OID\_PNP\_集\_电源将网络适配器设置为工作电源状态，而微型端口驱动程序未能通过此 OID，NDIS 假设设备处于不可恢复的状态。

若要支持网络唤醒事件，微型端口驱动程序还必须支持[oid\_PNP\_启用\_唤醒\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up) "oid"。 协议驱动程序和 NDIS 都使用此 OID 启用网络适配器的唤醒功能。 有关详细信息，请参阅[启用唤醒事件](enabling-wake-up-events.md)。

若要支持网络唤醒帧（请参阅[网络唤醒事件](network-wake-up-events.md)），微型端口驱动程序还必须支持与唤醒事件相关的下列 oid：

-   [OID\_PNP\_添加\_唤醒\_向上\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)

    协议驱动程序使用此 OID 将唤醒模式添加到网络适配器或微型端口驱动程序或两者维护的列表。

-   [OID\_PNP\_删除\_唤醒\_向上\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)

    协议驱动程序使用此 OID 删除以前通过 OID\_PNP 指定的唤醒模式\_添加\_唤醒\_向上\_模式。

支持网络唤醒事件的 NDIS 微型端口驱动程序可以选择支持以下与唤醒事件相关的统计 Oid：

-   [OID\_PNP\_唤醒\_\_错误](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-error)

    协议驱动程序将查询此 OID，以确定微型端口驱动程序的网络适配器发出信号的虚假唤醒的数目。

-   [OID\_PNP\_唤醒\_\_正常](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-wake-up-ok)

    协议驱动程序将查询此 OID，以确定微型端口驱动程序的网络适配器发出信号的有效唤醒的数目。

 

 





