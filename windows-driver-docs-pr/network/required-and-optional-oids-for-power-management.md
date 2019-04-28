---
title: 电源管理的必需和可选 OID
description: 电源管理的必需和可选 OID
ms.assetid: 147e35b2-dfa5-4238-82e6-5c48ffa30af5
keywords:
- Oid WDK 网络、 电源管理
- 唤醒功能 WDK 网络 Oid
- 电源管理 WDK NDIS 微型端口，Oid
- 对象标识符 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bdd38937b7f9f8fdbdbcfebaa94dd3443374d01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349353"
---
# <a name="required-and-optional-oids-for-power-management"></a>电源管理的必需和可选 OID





微型端口驱动程序，支持电源管理涉及到支持电源管理对象标识符 (Oid)。 微型端口驱动程序如何处理查询和 Oid 的集的详细说明，请参阅[Obtaining 和 SettingMiniport 驱动程序信息和对 WMI 的 NDIS 支持](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

有两个级别的微型端口驱动程序的电源管理支持：

1.  微型端口驱动程序可以支持的电源状态之间进行转换的网络适配器。 此支持仅电源管理支持的最低级别。 适用于网络适配器的设备的电源状态的说明，请参阅[设备的网络适配器的电源状态](device-power-states-for-network-adapters.md)。

2.  微型端口驱动程序还可以支持一个或多个[网络唤醒事件](network-wake-up-events.md)。

微型端口驱动程序在初始化期间报告电源管理功能。 有关在初始化期间报告的电源管理功能的详细信息，请参阅[ **NDIS\_微型端口\_适配器\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565920)和相关的属性的结构。

微型端口驱动程序必须支持以下 Oid，直接或中的电源状态之间进行转换的网络适配器的属性：

-   [OID\_PNP\_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff569774)

    中间驱动程序必须响应此 OID 查询。 NDIS 响应 OID\_PNP\_代表物理网络适配器的功能请求。 有关响应的中间驱动程序中此 OID 的详细信息，请参阅[处理即插即用事件和中间驱动程序中的电源管理事件](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)。

-   [OID\_PNP\_查询\_电源](https://msdn.microsoft.com/library/windows/hardware/ff569778)

    此 OID 指定到的网络适配器应准备转换，以便设备电源状态。 微型端口驱动程序必须始终返回 NDIS\_状态\_OID 的查询响应中的成功\_PNP\_查询\_电源。 通过返回 NDIS\_状态\_响应此 OID 的成功请求，微型端口驱动程序可保证它将转换的网络适配器上接收后续 OID 的指定的设备电源状态\_PNP\_设置\_POWER 请求。 微型端口驱动程序，在这种情况下，必须执行任何操作危害到太空船转换。

-   [OID\_PNP\_SET\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)

    此 OID 指示网络适配器必须转换为所指示的设备电源状态。 之前驱动程序返回 NDIS 微型端口驱动程序必须将网络适配器设置为指定的状态\_状态\_成功。 微型端口驱动程序必须始终返回 NDIS\_状态\_成功响应此 OID。 如果 OID\_PNP\_设置\_电源设置的网络适配器为工作电源状态和微型端口驱动程序失败，此 OID、 NDIS 假定设备处于不可恢复的状态。

若要支持网络唤醒事件，微型端口驱动程序还必须支持[OID\_PNP\_启用\_唤醒\_向上](https://msdn.microsoft.com/library/windows/hardware/ff569775)OID。 协议驱动程序和 NDIS 使用此 OID 来启用网络适配器的唤醒功能。 有关详细信息，请参阅[启用唤醒事件](enabling-wake-up-events.md)。

若要支持网络唤醒帧 (请参阅[网络唤醒事件](network-wake-up-events.md))，微型端口驱动程序还必须支持与唤醒事件相关的以下 Oid:

-   [OID\_PNP\_ADD\_WAKE\_UP\_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569773)

    协议驱动程序使用此 OID 将唤醒模式添加到网络适配器和/或微型端口驱动程序维护的列表。

-   [OID\_PNP\_REMOVE\_WAKE\_UP\_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569779)

    协议驱动程序将使用此 OID 删除唤醒它以前与指定模式相 OID\_PNP\_添加\_唤醒\_向上\_模式。

支持网络唤醒事件的 NDIS 微型端口驱动程序可以选择性地支持相关唤醒了下列统计 Oid 事件：

-   [OID\_PNP\_WAKE\_UP\_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569781)

    协议驱动程序查询此 OID 来确定 false 唤醒之后会通过微型端口驱动程序的网络适配器来发出信号的数目。

-   [OID\_PNP\_WAKE\_UP\_OK](https://msdn.microsoft.com/library/windows/hardware/ff569782)

    协议驱动程序查询此 OID 来确定有效的唤醒 ups 微型端口驱动程序的网络适配器的发送信号的数目。

 

 





