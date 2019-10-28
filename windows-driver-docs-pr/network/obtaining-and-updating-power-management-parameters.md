---
title: 获取和更新电源管理参数
description: 获取和更新电源管理参数
ms.assetid: 46c4d2ab-e6d9-4d23-bf40-0037b80b01af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ea9ffbcb9c2cfbb4cbb98d034f63557f4e08d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837748"
---
# <a name="obtaining-and-updating-power-management-parameters"></a>获取和更新电源管理参数





协议驱动程序可以使用[oid\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)OID 来查询当前启用的网络适配器的硬件功能。 成功从查询返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的指针。

协议驱动程序还可以将 OID\_PM\_参数用作集请求，以启用或禁用网络适配器的当前硬件功能。 协议驱动程序在 NDIS\_OID\_请求结构的**InformationBuffer**成员中提供指向 NDIS\_PM\_参数结构的指针。

**请注意**  协议驱动器无法禁用由其他协议驱动程序启用的功能。 如果没有任何协议驱动程序启用功能，则不会使用该功能。

 

**请注意**  NDIS 基于用户设置启用幻数据包和低功耗断开功能，并且这些功能不能由协议驱动程序禁用。

 

NDIS\_PM\_参数包括下列信息：

<a href="" id="enabledwolpacketpatterns"></a>**EnabledWoLPacketPatterns**  
包含对应于小型端口驱动程序在[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**SupportedWoLPacketPatterns**成员中报告的功能的标志。 例如，当网络适配器接收到位图、WOL 幻数据包或 EAP over LAN （EAPOL）请求标识符消息时，将会生成唤醒事件。 有关当前操作系统中可能的模式的完整列表，请参阅[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)引用页。

<a href="" id="enabledprotocoloffloads"></a>**EnabledProtocolOffloads**  
包含对应于小型端口驱动程序在[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**SupportedProtocolOffloads**成员中报告的功能的标志。 NDIS 使用这些标志在网络适配器上启用或禁用低功率协议卸载功能。 例如，启用了 IPv4 ARP、IPv6 邻居请求（NS）或 IEEE 802.11 可靠安全网络（RSN）4单向和双向握手的网络适配器卸载。 有关当前操作系统中支持的协议卸载的完整列表，请参阅[**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)引用页。

<a href="" id="wakeupflags"></a>**WakeUpFlags**  
包含 NDIS 用于启用或禁用网络适配器上的唤醒功能的标志。

对于 NDIS 6.20，NDIS\_PM\_唤醒\_\_链接上\_"启用了更改\_" 标志允许在链接更改时唤醒功能（media connect）。 有关此标志的详细信息，请参阅[低能耗媒体断开连接](low-power-on-media-disconnect.md)。

从 NDIS 6.30 开始，NDIS\_PM\_选择性\_挂起\_启用标志支持在基础 USB 网络适配器上支持 NDIS 选择性挂起。 有关详细信息，请参阅 " [NDIS 选择性挂起](ndis-selective-suspend.md)"。

当驱动程序将[oid 设置\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)OID 时，NDIS 完成请求，而不会将其转发给微型端口驱动程序。 NDIS 存储请求的设置，并将它们与其他此类请求中的设置组合在一起。

在 NDIS 将网络适配器转换为低功率状态之前，NDIS 会将 set 请求发送到包含 NDIS 存储的所有请求中的组合设置的微型端口驱动程序。 有关设置低功耗状态的详细信息，请参阅[LAN 唤醒的低功率](low-power-for-wake-on-lan.md)。

当前启用的功能可以是硬件支持的功能的子集。 有关硬件支持的功能的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

 

 





